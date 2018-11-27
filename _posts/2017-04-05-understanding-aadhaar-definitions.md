---
layout: post
title: "Understanding Aadhaar: Definitions &amp; Entities"
microblog: false
audio: 
photo: https://cdtestweb.files.wordpress.com/2017/04/a3535-1viawjjzlxqi4anotuqouwa2x.jpeg
date: 2017-04-05 10:55:58 +0400
guid: http://chirag.micro.blog/2017/04/05/understanding-aadhaar-definitions.html
---
<p>Aadhaar was established as a national Unique Identification number (UID) system. The Unique Identification Authority of India (UIDAI) falls under the purview of the Ministry of Electronics &amp; Information Technology (MeitY), and is audited by the Comptroller &amp; Auditor General (CAG).</p>
<p>This post attempts to review Aadhaar as the verifiable identification and authentication system in India based on a review of relevant provisions within the Aadhaar Act, 2016 and its Regulations.</p>
<p>The next post <a href="https://ekdrishti.in/understanding-aadhaar-data-security-85d361d47f72" target="_blank">covers data security</a>.</p>
<pre><a href="#4e42">Authentication &amp; Working</a><br><a href="#99da">Penalties</a><br><a href="#82a0">Did you know?</a><br><a href="#a8d3">Aadhaar Entities</a><br><a href="#6c3e">Aadhaar Act, 2016</a><br><a href="#0cd7">Grievance Redressal</a><br><a href="#26e3">References</a></pre>
<h3>Authentication &amp; Working</h3>
<p>Authentication — the ability to know that you are who you say you are before giving you access to something — is a fundamental tenet in information security. Credibility is infinitely improved when an authorized service provider can genuinely validate you, compared to receiving a photocopy of your passport. In return, you are guaranteed no one else is receiving a service or benefit to which you are entitled.</p>
<p>With this understanding, we explore the Aadhaar concept — a one-way authentication service. A service provider can authenticate you on a) your Aadhaar number and b) either OTP or biometrics, and deliver a service or a subsidy to you. The Aadhaar network does not communicate out of turn with the service provider though, and is not aware of what service was provided to you<a href="#df6d">¹</a>. It only knows which service provider requested your authentication, and logs this for audit purposes.²</p>
<figure class="wp-caption">

<img src="https://cdtestweb.files.wordpress.com/2017/04/6b158-1pns2lsaaxdn7o7n3ds9vfa.png">

<figcaption class="wp-caption-text">All Aadhaar authentication is initiated by the user via the relevant agency.</figcaption></figure><p>To use a specific example, here’s what a headline like ‘mobile phones will now be linked to Aadhaar’ means: instead of storing photocopies of your driver’s license or passport, the telecom provider (via an authorized service agency, explained below) requests authentication using Aadhaar, and upon receiving a ‘Yes’ issues you a SIM.</p>
<ul>
<li>Aadhaar logs when the telecom provider asked for your authentication, that it was successful</li>
<li>The service agency logs the same details but does not save (by law) any other data</li>
<li>The telecom provider logs the request and the result, and services that were delivered. It does not see any other data used for authentication.</li>
</ul>
<p>This concept is similar to credit card payments, where the service provider requests to charge you via a payment gateway. The gateway collects &amp; transmits your card details to the issuing bank, both of which only aware of the provider and the total charge. The service provider also does not see your credit card number.</p>
<h4>Aadhaar data</h4>
<p>Aadhaar’s core data infrastructure is called The Central Information Data Repository (CIDR). No details regarding its location or type of systems is available.</p>
<p>The CIDR is classified as a Protected System³ under the IT Act, 2000, a Critical Information Infrastructure (CII) by the NCIIPC⁴ and the UIDAI itself is ISO27001:2013 certified⁵.</p>
<p>Key facts regarding the data stored within the CIDR:</p>
<ul>
<li>Name, date of birth, address, gender, and (optional) mobile/email constitute <em>demographic information</em>.</li>
<li>Race, religion, caste, tribe, ethnicity, language, records of entitlement (benefits/subsidies), income or medical history are excluded by law.⁶</li>
<li>Photograph, fingerprints &amp;/or iris scan constitute <em>biometric information</em>.</li>
<li>Of this, fingerprints &amp; eye scan data are <em>core biometric data</em>, and excluded by law from being shared with “anyone for any reason whatsoever”.⁷ ⁸</li>
<li>Biometric data is also ‘sensitive personal data or information’ status per IT Act, 2000.⁹</li>
<li>Demographic information and biometric information are partitioned into separate databases. A single database does not have all of a holder’s information.</li>
</ul>
<p>For the Government to request anyone’s Aadhaar logs within the CIDR, it must be:</p>
<ul>
<li>in the “interest of national security”</li>
<li>directed by an officer with minimum rank of Joint Secretary</li>
<li>reviewed by an Oversight Committee consisting of 1 Cabinet Secretary and secretaries of the Department of Legal affairs &amp; the Department of Electronics &amp; Information Technology.¹⁰</li>
<li>pursuant to an order of a court not lower than a District Judge.</li>
</ul>
<p>Such an order is valid for a period of 3 months, with a possible 3 month extension which must be reviewed by the Oversight Committee.</p>
<h4>De-duplication¹¹</h4>
<p>During enrollment, an applicant’s data is validated against the CIDR to ensure that the holder was not previously issued an Aadhaar number, a process known as de-duplication.</p>
<p>Aadhaar de-duplication is mandated by Regulation and is performed using 3 different biometric algorithm softwares.¹²</p>
<h3>Penalties</h3>
<p>The penalty clauses under the Aadhaar Act provides for¹³:</p>
<ul>
<li>A 3-year term and/or a fine of Rs. 10,000 for impersonation, an attempt to impersonate during enrollment or to change identity information</li>
<li>A 3-year term and/or Rs. 10,000 fine for individuals and Rs. 1,00,000 for companies for unauthorized collection of identity information, intentionally disclosing, transmitting, copying of information</li>
<li>A 3-year term and a minimum fine of Rs. 10,00,000 for unauthorized access or attempt to access, download or any play with data within the CIDR</li>
<li>For companies, each person in charge of, or responsible to the company are also considered guilty unless they can prove otherwise.</li>
<li>All penalties apply over and above any other penalties charged (such as under the IT Act, 2000 or the Indian Penal Code)</li>
</ul>
<hr>

<h3>Did you know?</h3>
<h4>Biometric Lock</h4>
<p>An Aadhaar holder can place a permanent lock on biometric data after which it cannot be used for authentication. This lock can be temporarily removed ahead of a legitimate authentication request, and is automatically locked again once the request is completed or after a specific time, whichever is earlier.¹⁴ When locked, an authentication request results in a ‘No’ response.</p>
<h4>Virtual ID</h4>
<p>You can generate a 16-digit randomized Virtual ID to be used for authentication requests instead of your Aadhaar ID. This allows you to mask your original Aadhaar from the provider while still using it for identification. All providers must accept Virtual IDs for services by June 2018.</p>
<h4>Consent</h4>
<p>The Aadhaar Act mandates that consent of the holder must be taken and recorded for enrollment or an authentication request. The holder must be also be informed about the purpose for which authentication is being requested. Failure to do so is a violation of the Act and can be penalized.¹⁵</p>
<hr>

<h3>Entities</h3>
<p>There are three types of entities which share a technology relationship with the CIDR:</p>
<ul>
<li>Authentication Service Agency (ASA), 27: Entities with established 1-to-1 secure leased line/MPLS connectivity with the CIDR, regulated directly by the UIDAI to provide authentication services.</li>
<li>Authentication User Agency (AUA), 350: Entities that provide services based on Aadhaar-based authentication performed by a registered ASA¹⁶.</li>
<li>Electronic Know Your Customer (e-KYC), 271: Entities that perform KYC using Aadhaar. e-KYC, upon successful authentication, receive a digitally signed response containing encrypted demographic information and photograph for instant, non-repudiable KYC.</li>
</ul>
<p>The current live list of Aadhaar entities is <a href="https://uidai.gov.in/images/list_of_live_asa_aua_ksa_kua.pdf" target="_blank">available here</a>, and seems to be updated once a month. Holders are encouraged to ensure they are providing consent to entities on this list alone.</p>
<p>A full breakdown of the ASA-AUA ecosystem, along with the framework to transmit data, is forthcoming.</p>
<h3>Aadhaar Act, 2016</h3>
<p>The Aadhaar (Targeted Delivery of Financial and Other Subsidies, Benefits &amp; Services) Act, 2016 provides legislative backing to Aadhaar as the national unique identification mechanism in the Country¹⁷. The Act superceeds the <a href="https://uidai.gov.in/images/bill_for_national_identification_authority_of_india_13012017.pdf" target="_blank">The Bill for National Identification Authority of India, 2010</a>.</p>
<p>The Aadhaar Act 2016 also provides clear definitions and processes for enrolment, core biometric data specifications, authentication, audits, overall protection of information and the responsibilities of the UIDAI.</p>
<p>As of the writing of this post, Aadhaar cards for non-residents and Overseas Citizens of India (OCI) holders is still in the works. No timeframe for this is yet available¹⁸.</p>
<h4>Alternative ID</h4>
<p>A person who does not have an Aadhaar card but is entitled to any benefit paid from the Consolidated Fund of India will not be denied this benefit until his Card is issued, provided an alternative means of identification is made available to the entity in question¹⁹.</p>
<hr>

<p>As of the time of writing this post, 113 crore Aadhaar cards have been issued, and the last five years have witnessed over 400 crore authentication transactions²⁰.</p>
<p>Caution when it pertains to data privacy is both desirable and needed. Aadhaar is an ambitious program that seeks to provide a unified, unique, non-repudiable and verifiable form of identity to millions at a near incomparable scale. The world is taking clear notice of this development. As <a href="https://medium.com/u/d22fa00ce21f" target="_blank">Vivek Wadhwa</a>— distinguished fellow with Carnegie Mellon University — highlights, <a href="https://ekdrishti.in/vivek-wadhwa-america-has-much-to-learn-from-india-aadhaar-a-game-changer-3bda809f00a9?source=---------2" target="_blank">India is pioneering something the West can learn from</a>:</p>
<blockquote>The instant and non-repudiable proof of identity that Aadhaar’s know your customer technology, e-KYC, provides, gives India a big advantage. Most people in the US have drivers licenses and social security numbers. But these are not verifiable with biometrics or mobile numbers, so complex verification technologies need to be built into every financial system. Indian entrepreneurs building applications don’t need to worry about all this.</blockquote>
<p>Beyond entrepreneurs, the fact that schemes or benefits can be rolled out by governments (both Centre and states) without the need to build separate complex infrastructures which then witness on-boarding delays clearly have numerous benefits.</p>
<p>Some of this is already visible, with <a href="http://www.hindustantimes.com/india-news/aadhaar-data-base-fully-safe-and-secure-says-uidai/story-rMkGys9n1UMnzyKO04BAeM.html" target="_blank">Government estimates of Rs. 50,000 crore leakages being plugged so far</a>. The system has helped root out ‘ghosts’ within the system as well, where <a href="https://ekdrishti.in/87-lakh-mnrega-job-cards-removed-54bad536316d?source=---------0" target="_blank">87 lakh unknown MNREGA job cards were removed</a> or that <a href="https://ekdrishti.in/4-4-lakh-ghost-students-in-jharkhand-manipur-andhra-pradesh-bf50600d3564?source=---------0" target="_blank">4.4 lakh students in just 3 states only existed on paper</a>.</p>
<p>That said, we must look at the law and the implementation ecosystem to determine whether enough has been done to ensure security, and alleviate privacy concerns of the citizens who will need to subscribe to the national ID.</p>
<p>Legally, The Aadhaar Act, 2016 and expansive Regulations for Enrolment, Authentication, Data Security &amp; Sharing of Information, are serious attempts to tighten legislation and processes related to Aadhaar usage. A first-glance comparison indicates that the 2016 Act is a far cry away — particularly in terms of handling of biometric data, and privacy — from the Bill that was tabled in 2010. For example, under the 2010 Bill, sharing biometric data outside the CIDR would have been perfectly legal.</p>
<p>In some (perhaps, many) ways, the attention and eyeballs on Aadhaar is a good thing, where even the smallest flaw would put the credibility of Aadhaar at stake, and should keep the men and women behind Aadhaar on their toes, as they should be.</p>
<hr>

<h4>Thoughts</h4>
<ul>
<li>What happens to Aadhaar data upon death? While logs and data itself should be maintained pursuant to legal requirements, a straightforward way to permanently lock (with no option for temporary unlock thereafter) a deceased person’s biometric data should be made available.</li>
<li>There is ample protection under law for violation by any entity — authorized or unauthorized — that performs unauthorized actions within the Aadhaar framework. No statistics around timeframe to resolving grievances is available at the moment. Beyond grievance redressal, should a special Court or Tribunal be instituted specifically for Aadhaar?</li>
<li>It makes logistical sense that that UIDAI has engaged with enrollment agencies to help with Aadhaar dispensation. Now that enrolment has crossed 95%, should the UIDAI consolidate the enrolment ecosystem and annex it within direct control of the UIDAI?</li>
</ul>
<hr>

<h4>Grievance Redressal</h4>
<p>As of today, online grievances may be submitted via the <a href="http://pgportal.gov.in/GrievanceNew.aspx" target="_blank">Centralized Public Grievance Redressal System</a>.</p>
<figure class="wp-caption">

<img src="https://cdtestweb.files.wordpress.com/2017/04/a3535-1viawjjzlxqi4anotuqouwa2x.jpeg">

<figcaption class="wp-caption-text">The Central Public Grievance Redressal System allows you to register grievances with the UIDAI</figcaption></figure><p>Additionally, a contact centre has been established:</p>
<ul>
<li>Voice: 1947</li>
<li>Email: <a href="mailto:help@uidai.gov.in" target="_blank">help@uidai.gov.in</a>
</li>
<li>PO Box 1947, GPO Bengaluru 560 001</li>
</ul>
<p>Grievances can also be addressed through regional offices in Bengaluru, Chandigarh, New Delhi, Guwahati, Hyderabad, Lucknow, Mumbai &amp; Ranchi.</p>
<hr>
<p><em>Updated 10 Jan 2018 to include information about Virtual ID and limited KYC.</em></p><hr>

<h4>Notes</h4>
<p><a href="#b30e">[1]</a> <a href="https://uidai.gov.in/images/targeted_delivery_of_financial_and_other_subsidies_benefits_and_services_13072016.pdf" target="_blank">The Aadhaar (Targeted Delivery of Financial and Other Subsidies, Benefits and Services) Act, 2016</a> Section 32 (3). See also <a href="https://uidai.gov.in/images/loksabha/1281.pdf" target="_blank">Lok Sabha Unstarred Question 1281, answered 23 Nov 2016</a>.</p>
<p>[2] Logs must be maintained by the service provider &amp; the authentication agency for (2) years during which the holder may request the logs, followed by an archive for 5 years. The UIDAI maintains logs for a period of (6) months during which they can be accessed by the holder, followed by archiving them for 5 years. Ref: <a href="https://uidai.gov.in/images/regulation_1_to_5_15092016.pdf" target="_blank">Aadhaar (Authentication) Regulations, 2016 (No. 3 of 2016) Chapters III, IV</a></p>
<p>[3] Protected System or a Critical Information Infrastructure (CII), per The <a href="http://meity.gov.in/content/view-it-act-2000" target="_blank">Information Technology Act, 2000</a> <a href="http://meity.gov.in/content/offences" target="_blank">Section 70</a>, is a computer resource, the incapacitation or destruction of which, shall have a debilitating impact on national security, economy, public health of safety. Accessing or even attempting to access a Protected System is punishable with a 10 year term and/or a fine.</p>
<p>[4] Any attack on information assets classified as CII is considered an act of cyber terrorism. Ref: <a href="http://www.digitalpolicy.org/nciipc-evolving-framework/" target="_blank">Datta, Saiket: The NCIIPC &amp; its evolving framework</a></p>
<p>[5] The ISO/IEC 27001:2013 Information Security Management System (ISMS) Certification is the latest version of the global information security standard covering information security controls and their management systems. The UIDAI is certified by the Standarisation Testing &amp; Quality Certification (STQC), a Directorate of the MeitY, an internationally recognized Assurance Service. Ref: <a href="https://uidai.gov.in/images/loksabha/1777.pdf" target="_blank">Lok Sabha Unstarred Question № 1777, answered 4 May 2016</a>.</p>
<p>[6] Aadhaar Act, 2016 Section 2 (k)</p>
<p>[7] Aadhaar Act, 2016 Section 29 (1)(a)</p>
<p>[8] In August 2016, the State Government of Rajasthan requested the UIDAI for demographic information of residents with the Government, which was refused by the UIDAI. The UIDAI suggested the Government could request to become an authorized eKYC provider to allow for authentication/KYC with necessary consent of the holder but not as a demographic data collector. Ref: <a href="https://uidai.gov.in/images/loksabha/2369.pdf" target="_blank">Unstarred Question № 2369, answered 30 Nov 2016</a>.</p>
<p>[9] Aadhaar Act, 2016 Section 30 (c)</p>
<p>[10] Aadhaar Act, 2016 Section 33. The order, if issued, is valid for 3 months, and may be extended by a further 3 months if approved by the Oversight Committee.</p>
<p>[11] <a href="https://uidai.gov.in/images/regulation_1_to_5_15092016.pdf" target="_blank">Aadhaar (Enrolment &amp; Update) Regulations, 2016</a> Section 13 (2)</p>
<p>[12] <a href="https://uidai.gov.n/images/aadhaar_question_and_answers.pdf" target="_blank">UIDAI: Facts about Aadhaar</a></p>
<p>[13] Aadhaar Act, 2016 Sections 39–42, Section 43(1), Section 46 for penalties</p>
<p>[14] <a href="https://uidai.gov.in/images/regulation_1_to_5_15092016.pdf" target="_blank">Aadhaar (Authentication) Regulations, 2016</a> Section 11</p>
<p>[15] Aadhaar Act, 2016 Sections 3 (2), 8 (2)</p>
<p>[16] The exception being an AUA that is also an ASA, but then they’d be undergoing the same authorization and certification as other ASAs.</p>
<p>[17] Except in Jammu &amp; Kashmir</p>
<p>[18] <a href="https://uidai.gov.in/images/loksabha/18.pdf" target="_blank">Lok Sabha Unstarred Question № 18, answered 24 Feb 2016</a></p>
<p>[19] Aadhaar Act, 2016 Section 7</p>
<p>[20] <a href="https://ekdrishti.in/the-aadhaar-breach-61cf2774d853" target="_blank">As stated by the UIDAI</a></p>
