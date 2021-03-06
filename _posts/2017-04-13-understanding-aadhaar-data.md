---
layout: post
title: "Understanding Aadhaar: Data Security"
microblog: false
audio: 
photo: https://cdtestweb.files.wordpress.com/2017/04/24d5a-1is2pyyb6aszme_sokuc80g.jpeg
date: 2017-04-13 15:49:59 +0400
guid: http://chirag.micro.blog/2017/04/13/understanding-aadhaar-data.html
---
<figure>

<img src="https://cdtestweb.files.wordpress.com/2017/04/24d5a-1is2pyyb6aszme_sokuc80g.jpeg">
</figure><p>This is part 2 of the Aadhaar series, following Definitions &amp; Entities:</p>
[embed]https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38[/embed]
<p>This post performs a quick dive into the technology-based and process-based security provisions of Aadhaar data.</p>
<pre><a href="#b380">Data Access</a><br><a href="#60d8">Process</a><br><a href="#f800">Data Security</a><br><a href="#5862">Notes</a></pre>
<hr>

<h3>
<code>Data </code>Access</h3>
<p>The core Aadhaar infrastructure is called the Central Information Data Repository (CIDR). There are two main purposes for which data is accessed from the CIDR: Authentication &amp; e-KYC.</p>
<p><em>For an explanation on the different entities and their relationships within the Aadhaar ecosystem, please see </em><a href="https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38#a8d3" target="_blank"><em>our section on Aadhaar entities</em></a><em>.</em></p>
<h4>Authentication</h4>
<p>A vendor can use Aadhaar authentication to verify you before offering services. This process utilizes your Aadhaar number and either your OTP or biometrics as a second factor to authenticate you. Vendors who use Aadhaar authentication services are authorized by the UIDAI as Authorized User Agencies (AUAs). Each AUA must use an Authorized Service Agency (ASA) — the only entities allowed to connect to the CIDR. The authentication process is explained in more detail <a href="https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38#4e42" target="_blank">here</a>.</p>
<p>In response, the CIDR returns a digitally signed ‘Yes/No’ depending on the success of the authentication request.</p>
<h4>Electronic Know Your Customer (e-KYC)</h4>
<p>A vendor can use Aadhaar for the purpose of instant electronic KYC. Just like authentication entities, e-KYC entities must be authorized by the UIDAI, and utilize KSAs (ASAs with KYC permissions) — the only entities allowed to use the e-KYC connection endpoints.</p>
<p>In response, the CIDR returns a digitally signed and encrypted demographic record (name, gender, address, etc) and photograph block¹. In January 2018, a ‘limited KYC’ was introduced where only need-based details would be shared with the authorised agencies.</p>
<h4>APIs</h4>
<p>Application Programming Interfaces (APIs) are the industry-standard method to connect to systems. They allow the issuing entity (in this case, the UIDAI) to maintain control over what information — and in what manner — is shared with the requestor. APIs adds a layer of encapsulation by limiting what is available to the ‘outside’ via targeted requests, thus not requiring any direct access to a data store or database (DB).</p>
<p>For example, let’s say you wish to know how many steps I’ve walked on a day, which I log in a DB. Rather than give you direct access to my DB—which also contains other data which you don’t require, nor do I want to share—I give you an API request endpoint, validated by a key:</p>
<pre>[me.example/getSteps](https://me.example/getSteps?authKey=45aedlfkja359874425)</pre>
<p>which returns:</p>
<pre>{ “steps”: 372 } </pre>
<p>Similarly, the Aadhaar authentication service is done over a URL endpoint²:</p>
<pre>https://&lt;host&gt;/&lt;version&gt;/&lt;AUA code&gt;/&lt;uid digit 0&gt;/&lt;uid digit 1&gt;/&lt;ASA license key&gt;</pre>
<p>A separate API is used for eKYC or enrolment. The production server hosts are only shared with the ASAs and are not available online. As such, the API endpoints are not accessible over the internet.</p>
<p>The request format for an authentication request is as follows³:</p>
<pre>&lt;Auth uid=”” rc=”” tid=”” ac=”” sa=”” ver=”” txn=”” lk=””&gt; <br>&lt;Uses pi=”” pa=”” pfa=”” bio=”” bt=”” pin=”” otp=””/&gt; <br>&lt;Meta udc=”” rdsId=”” rdsVer=”” dpId=”” dc=”” mi=”” mc=”” /&gt; <br>&lt;Skey ci=””&gt;encrypted and encoded session key&lt;/Skey&gt; <br>&lt;Hmac&gt;SHA-256 Hash of Pid block, encrypted and then encoded&lt;/Hmac&gt; &lt;Data type=”X|P”&gt;encrypted PID block&lt;/Data&gt; <br>&lt;Signature&gt;Digital signature of AUA&lt;/Signature&gt; &lt;/Auth&gt;</pre>
<p>The request only shares meta-data comprising the device information, AUA signature, etc. and the encrypted PID block. Information such as details of the service being provided, or any details about the holder do not form part of the request. Even if a service provider were to pass such information — and it would be illegal to do so — the only blocks and variables recognized by the CIDR are the ones in the above request.</p>
<h4>PID Block</h4>
<p>When a registered device is called by the application, it captures, processes and encodes the digitally signed biometric record⁴.</p>
<pre>Bh=SHA-256(bio_record) <br>Be=DSA(Bh+timestamp+unique_device_code,device_private_key)</pre>
<p>This is used to finally create the signed &amp; encoded biometric record:</p>
<pre>Bs=base64(Be)</pre>
<p>A Device Info Hash (dih) is also included as part of the PID block:</p>
<pre>dih = SHA-256(device_provider_id+device_service_id+device_version+unique_device_code+model_id+idHash)</pre>
<p>The <code>idHash</code> is an encrypted device ID which must match the hash shared with the CIDR when the device was registered. A separate <code>wadh</code> (wrapper API data hash) is also used for eKYC transactions.</p>
<p>In this way, the PID block is created and encrypted on the registered device itself and the process is independent of the AUA application. The biometric record is encrypted using a 256-bit symmetric encryption session key (AES/GCM/No padding). The one-time use session key is then encrypted asymmetrically (RSA/ECB/PKCS1Padding) with a 2048-bit UIDAI-issued public key, making the CIDR the sole entity that can decrypt the record.</p>
<hr>

<h3>Process</h3>
<p>Once created, the PID block is then signed with the AUAs digital key and passed to the ASA. The ASA then makes the API call, along with its own unique digital identifiers and a success or failure response is returned.</p>
<p>Each device must be registered with the UIDAI along with the device provider’s ID, a unique identifier (serial number), a digitally signed certificate, along with the provider’s key issued by the UIDAI⁵. All of these details are part of the meta-data of the authentication or eKYC request.</p>
<p>Currently, the UIDAI is in process to increase the CIDR’s authentication capacity to 10 crore transactions per day⁶.</p>
<hr>

<h3>Data Security</h3>
<p>To recap, your fingerprint and/or eye scan data are classified as core biometric information and has a one-way ticket into the CIDR. By law, core biometric information collected shall not be shared “with anyone for any reason whatsoever”⁷.</p>
<p>As highlighted in the <a href="https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38#8ab4" target="_blank">previous post</a>, the CIDR is classified as a Protected System under the IT Act, 2000, a Critical Information Infrastructure (CII) by the NCIIPC and the UIDAI itself is ISO27001:2013 certified.</p>
<p>The following are some of the security enforcements across the Aadhaar ecosystem:</p>
<ul>
<li>There is no connection endpoint that returns a holder’s biometrics, as required by law⁸.</li>
<li>Demographic information and biometric information are partitioned into separate databases secured between firewalls; a single database does not have all the user’s data in one physical location⁹. Raw biometric data is stored in encrypted form within the CIDR.</li>
<li>Connection to the CIDR is only available to ASAs (27 entities at this time) over 1-to-1 leased line or MPLS¹⁰ links, i.e., not over the internet.</li>
<li>Each ASA is allotted a separate DMZ¹¹.</li>
<li>The PID block is encrypted with AES-256 using a one-time session key. The session key is then encrypted with a 2048-bit UIDAI issued key. This makes it extremely expensive to break¹².</li>
<li>The PID block includes a timestamp and a one-time session key to prevent reuse.</li>
<li>The digital keys of the registered device, the AUA and the ASA are logged and validated for every transaction.</li>
<li>The session key used for the PID block must not be stored and should not be reused across transactions¹³.</li>
<li>GCM encryption¹⁴ was added in API v2.0</li>
<li>Network connectivity between the ASA and AUA must be secured via a leased line or at least a VPN/SSL. It is the ASA’s responsibility to ensure this connectivity requirement.</li>
<li>Multi-factor authentication (using Aadhaar number + biometrics + OTP) is also available over the API. This is not mandatory as a phone number is not required for Aadhaar enrolment.</li>
<li>In cases where self-service is not possible and operator interference is required to operate a device, the operator must be authenticated and their Aadhaar number logged to perform any functions.</li>
<li>ASA and registered devices do not store PIB blocks beyond a few seconds in cache for buffering. Device applications and ASAs are verified by the UIDAI directly.</li>
<li>Enrolment client software is entirely written, maintained and provided directly by the UIDAI.</li>
<li>All meta-data of a request — timestamp, the entities involved — are made available online for 6 months, and archived for 7 years by law¹⁵.</li>
<li>The CIDR in its entirety is located inside India and all authentication requests route within the Country.</li>
<li>The Aadhaar number itself is random and is not based on any identifying personal factors of the holder¹⁶.</li>
<li>In January 2018, the UIDAI provides the option to generate a further randomized 16-digit Virtual ID for authentication requests so that users do not need to share their Aadhaar ID with providers. There are no limit to generating new Virtual IDs for the same Aadhaar, the old one is automatically discontinued once a new ID is generated.</li>
</ul>
<hr>

<h4>Notes</h4>
<p>[1] Aadhaar does not independently verify addresses submitted as part of enrollment. However, it should be noted that Aadhaar only accepts otherwise verifiable proof of address (such as a passport, electricity bill, water bill within 3 months old, bank statement, etc).</p>
<p>[2] <a href="https://uidai.gov.in/images/FrontPageUpdates/aadhaar_authentication_api_2_0_1.pdf#page9" target="_blank">Explanation of authentication API request URL</a></p>
<p>[3] <a href="https://uidai.gov.in/images/FrontPageUpdates/aadhaar_authentication_api_2_0_1.pdf#page11" target="_blank">Explanation of authentication API request parameters</a></p>
<p>[4] <a href="https://uidai.gov.in/images/resource/aadhaar_registered_devices_2_0_09112016.pdf#page9" target="_blank">Registered device PID block specification</a></p>
<p>[5] <a href="https://uidai.gov.in/images/resource/aadhaar_registered_devices_2_0_09112016.pdf#page8" target="_blank">Device registration process</a></p>
<p>[6] <a href="https://uidai.gov.in/images/loksabha/LS_USQ_5064_answered_on_05042017.pdf" target="_blank">Lok Sabha unstarred question № 5064, answered 4 April 2017</a></p>
<p>[7] The only exception under law is in the interest of ‘national security’, which <a href="https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38#ef5f" target="_blank">requires approval by an Oversight Committee and a court order</a>.</p>
<p>[8] Aadhaar Act, 2016 Section 29 (a)</p>
<p>[9] <a href="https://uidai.gov.in/images/aadhaar_question_and_answers.pdf#page3" target="_blank">Facts about Aadhaar, UIDAI</a></p>
<p>[10] Multiprotocol Label Switching (MPLS) is a unidirectional tunnel between a pair of routers, making it a 1:1 network between a source and a destination, not exposed to anyone else.</p>
<p>[11] <a href="https://authportal.uidai.gov.in/static/d3_4_security_policy_framework_v1.pdf" target="_blank">Security Policy &amp; Framework for UIDAI Authentication</a></p>
<p>[12] An RSA study titled <a href="https://japan.emc.com/emc-plus/rsa-labs/historical/a-cost-based-security-analysis-key-lengths.htm" target="_blank">A cost-based security analysis of symmetric and asymmetric key lengths</a>, published in 2000, concludes that it would take about 3 million years to break a 1020-bit key with US$10 million being available for hardware. Scaling further, it concludes a 128-bit symmetric key (equivalent to a 1620-bit asymmetric RSA key) — with a budget of $US10 trillion — would require 10¹⁰ years (for context, the age of the universe is estimated to be 1.38•10¹⁰ years).</p>
<p>A <a href="http://www.ecrypt.eu.org/ecrypt2/documents/D.SPA.20.pdf" target="_blank">2011–12 yearly report</a> by the European Network of Excellence in Cryptology II (Encrypt II) rates a 256-bit key as adequate protection for the “foreseeable future”, affording good production even against quantum computers.</p>
<p>Additionally, the <a href="https://www.enisa.europa.eu/publications/algorithms-key-size-and-parameters-report-2014/at_download/fullReport#page27" target="_blank">Algorithms, key size and parameters report – 2014</a> by the European Union Agency for Network &amp; Information Security (ENISA) notes:</p>
<ul>
<li>AES is classified as “the block cipher of choice for future applications”, with a recommended minimum size of 128-bits. An attack on AES-256 is rated as requiring time 2⁹⁹ and data complexity 2⁹⁹, such that related keys are used (and therefore, requiring more time if keys are randomly selected). Breaking AES-256 is expected to require 2²⁵⁴ encryption operations and 2⁸⁰ plaintexts.</li>
<li>SHA-256, used for building the Device Info Hash is classified as “future use” hash function.</li>
</ul>
<p>[13] The only re-use of the session key is allowed when used as a ‘seed key’ during a synchronised key scheme session. In this case, an AES session key is generated and can be reused until the session is completed (or 4 hours, whichever is earlier).</p>
<p>[14] <a href="http://csrc.nist.gov/groups/ST/toolkit/BCM/documents/proposedmodes/gcm/gcm-spec.pdf" target="_blank">Galois/Counter Mode</a> encryption was added to Aadhaar authentication requests in 2016. See the API documentation for <a href="https://uidai.gov.in/images/FrontPageUpdates/aadhaar_authentication_api_2_0_1.pdf#page31" target="_blank">how Aadhaar uses GCM encryption</a>.</p>
<p>[15] <a href="https://ekdrishti.in/understanding-aadhaar-definitions-entities-5adc587c7e38#p922d" target="_blank">Aadhaar (Authentication) Regulations, 2016 Chapters III, IV</a></p>
<p>[16] Aadhaar Act, 2016 Section 4(2)</p>
