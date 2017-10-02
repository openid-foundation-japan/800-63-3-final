
<div class="text-right" markdown="1">

# <a name="800-63b"></a> NIST Special Publication 800-63B

![](sp800-63-3/media/div-1.png)  

# Digital Identity Guidelines (翻訳版)

### _Authentication and Lifecycle Management_

![](sp800-63-3/media/div-2.png)  

Paul A. Grassi    
James L. Fenton    
Elaine M. Newton    
Ray A. Perlner    
Andrew R. Regenscheid    
William E. Burr    
Justin P. Richer  

**Privacy Authors:**  
Naomi B. Lefkovitz  
Jamie M. Danker  

**Usability Authors:**  
Yee-Yin Choong      
Kristen K. Greene      
Mary F. Theofanos   

This publication is available free of charge from:    
https://doi.org/10.6028/NIST.SP.800-63b    


![](sp800-63-3/media/csd.png)  
![](sp800-63-3/media/nist_logo.png)

</div><div class="breaker text-right" markdown="1">

# NIST Special Publication 800-63B

# Digital Identity Guidelines

### Authentication and Lifecycle Management

<table class="authors">
  <tr>
    <td>Paul A. Grassi<br>Elaine M. Newton<br><i>Applied Cybersecurity Division</i><br><i>Information Technology Laboratory</i></td>
    <td><strong>Privacy Authors:</strong><br>Naomi B. Lefkovitz<br><i>Applied Cybersecurity Division</i><br><i>Information Technology Laboratory</i></td>
  </tr>
  <tr>
	<td>Ray A. Perlner<br>Andrew R. Regenscheid<br><i>Cybersecurity Division</i><br><i>Information Technology Laboratory</i></td>
	<td>Jamie M. Danker<br><i>National Protection and Programs Directorate</i><br><i>Department of Homeland Security</i></td>
  </tr>
  <tr>
	<td>James L. Fenton<br><i>Altmode Networks</i><br><i>Los Altos, CA</i></td>
	<td><strong>Usability Authors:</strong><br>Yee-Yin Choong<br>Kristen K. Greene<br><i>Information Access Division</i><br><i>Information Technology Laboratory</i></td>
  </tr>
  <tr>
    <td>William E. Burr<br><i>Dakota Consulting, Inc.</i><br><i>Silver Spring, MD</i></td>
    <td>Mary F. Theofanos<br><i>Office of Data and Informatics</i><br><i>Material Measurement Laboratory</i></td>
  </tr>
  <tr>
  	<td colspan="2">Justin P. Richer<br><i>Bespoke Engineering</i><br><i>Billerica, MA</i></td>
  </tr>
</table>

### 翻訳者

Tatsuya Katsuhara (勝原 達也)  
*NRI SecureTechnologies, Ltd.*

Hitomi Kimura (木村 瞳)  
*Trend Micro Inc.*


This publication is available free of charge from:    
https://doi.org/10.6028/NIST.SP.800-63b    

June 2017

![](sp800-63-3/media/commerce_logo.png)

U.S. Department of Commerce  
*Wilbur L. Ross, Jr., Secretary*  

National Institute of Standards and Technology  
*Kent Rochford, Acting NIST Director and Under Secretary of Commerce for Standards and
Technology*

</div>

<div class="breaker"/>

<div class="text-center" markdown="1">

### Authority

</div>

This publication has been developed by NIST in accordance with its statutory responsibilities under the Federal Information Security Modernization Act (FISMA) of 2014, 44 U.S.C. § 3551 et seq., Public Law  (P.L.) 113-283. NIST is responsible for developing information security standards and guidelines, including minimum requirements for federal systems, but such standards and guidelines shall not apply to national security systems without the express approval of appropriate federal officials exercising policy authority over such systems. This guideline is consistent with the requirements of the Office of Management and Budget (OMB) Circular A-130.

Nothing in this publication should be taken to contradict the standards and guidelines made mandatory and binding on federal agencies by the Secretary of Commerce under statutory authority. Nor should these guidelines be interpreted as altering or superseding the existing authorities of the Secretary of Commerce, Director of the OMB, or any other federal official. This publication may be used by nongovernmental organizations on a voluntary basis and is not subject to copyright in the United States. Attribution would, however, be appreciated by NIST.

<div class="text-center" markdown="1">

National Institute of Standards and Technology Special Publication 800-63B  
Natl. Inst. Stand. Technol. Spec. Publ. 800-63B, 78 pages (June 2017)  
CODEN: NSPUE2

This publication is available free of charge from:  
https://doi.org/10.6028/NIST.SP.800-63b  

</div>

<div class="text-justify" markdown="1">
>Certain commercial entities, equipment, or materials may be identified in this document in order to describe an experimental procedure or concept adequately. Such identification is not intended to imply recommendation or endorsement by NIST, nor is it intended to imply that the entities, materials, or equipment are necessarily the best available for the purpose.
<br /><br />
>There may be references in this publication to other publications currently under development by NIST in accordance with its assigned statutory responsibilities. The information in this publication, including concepts and methodologies, may be used by federal agencies even before the completion of such companion publications. Thus, until each publication is completed, current requirements, guidelines, and procedures, where they exist, remain operative. For planning and transition purposes, federal agencies may wish to closely follow the development of these new publications by NIST.
<br /><br />
>Organizations are encouraged to review all draft publications during public comment periods and provide feedback to NIST. Many NIST cybersecurity publications, other than the ones noted above, are available at [http://csrc.nist.gov/publications/](http://csrc.nist.gov/publications/).
</div>

<div class="text-center" markdown="1">
**Comments on this publication may be submitted to:**    

National Institute of Standards and Technology  
Attn: Applied Cybersecurity Division, Information Technology Laboratory  
100 Bureau Drive (Mail Stop 2000) Gaithersburg, MD 20899-2000  
Email: <dig-comments@nist.gov>

All comments are subject to release under the Freedom of Information Act (FOIA).

</div>

<div class="text-center" markdown="1">

### Reports on Computer Systems Technology

</div>

The Information Technology Laboratory (ITL) at the National Institute of
Standards and Technology (NIST) promotes the U.S. economy and public
welfare by providing technical leadership for the Nation's measurement
and standards infrastructure. ITL develops tests, test methods,
reference data, proof of concept implementations, and technical analyses
to advance the development and productive use of information technology.
ITL's responsibilities include the development of management,
administrative, technical, and physical standards and guidelines for the
cost-effective security and privacy of other than national
security-related information in federal information systems. The Special
Publication 800-series reports on ITL's research, guidelines, and
outreach efforts in information system security, and its collaborative
activities with industry, government, and academic organizations.

<div class="text-center" markdown="1">

### 概要
<!--
### Abstract
-->

</div>

これらのガイドラインは, Digital Identityサービスを実装する連邦政府機関に対する技術的要件を提供し, この目的以外の標準の開発や利用を制限してはいない. これらのガイドラインは, オープンなネットワークを介して政府のシステムと相互作用するSubjectのAuthenticationに焦点を当て, 与えられたClaimantが以前にAuthenticateされたSubscriberであることを確認する.  Authenticationプロセスの結果は, Authenticationを行うシステムによってローカルで使用されたり, Federated Identity システムの他の場所でassertされたりすることがある.  このドキュメントでは, 3つのAuthenticator Assuarance Levelのそれぞれに対して技術要件を定義する.  この刊行物は, NIST Special Publication（SP）800-63-2の対応するセクションに優先するものである. 

<!--
These guidelines provide technical requirements for federal agencies implementing digital identity services and are not intended to constrain the development or use of standards outside of this purpose. These guidelines focus on the authentication of subjects interacting with government systems over open networks, establishing that a given claimant is a subscriber who has been previously authenticated. The result of the authentication process may be used locally by the system performing the authentication or may be asserted elsewhere in a federated identity system. This document defines technical requirements for each of the three authenticator assurance levels. This publication supersedes corresponding sections of NIST Special Publication (SP) 800-63-2.
-->

<div class="text-center" markdown="1">

### キーワード
<!--
### Keywords
-->

</div>

authentication; credential service provider; digital authentication; digital credentials; electronic authentication; electronic credentials, federation.

<div class="text-center" markdown="1">

### 謝辞
<!--
### Acknowledgements
-->

</div>

The authors gratefully acknowledge Kaitlin Boeckl for her artistic graphics contributions to all volumes in the SP 800-63 suite and the contributions of our many reviewers, including Joni Brennan from the Digital ID & Authentication Council of Canada (DIACC), Kat Megas, Ellen Nadeau, and Ben Piccarreta from NIST, and Ryan Galluzzo and Danna Gabel O'Rourke from Deloitte & Touche LLP.

The authors would also like to acknowledge the thought leadership and innovation of the original authors: Donna F. Dodson, W. Timothy Polk, Sarbari Gupta, and Emad A. Nabbus. Without their tireless efforts, we would not have had the incredible baseline from which to evolve 800-63 to the document it is today. In addition, special thanks to the Federal Privacy Council's Digital Authentication Task Force for the contributions to the development of privacy requirements and considerations.

<div class="text-center" markdown="1">

### 要求記法および規則
<!--
### Requirements Notation and Conventions
-->

</div>


「SHALL(するものとする)」及び「SHALL NOT(しないものとする)」という用語は, 刊行物に厳密に従うことを要求しており, 内容と異なってはならない. 

「SHOULD(すべきである)」及び「SHOULD NOT(すべきではない)」という用語は, いくつかある選択肢の中で特定の推奨があることを示しており, 他の選択肢については言及も除外もしない. ある行動指針を推奨するが, 必須であることまでは要求しない. (否定の意味では)ある選択肢または行動指針を非推奨するが, 禁止はしない. 

「MAY(してもよい)」及び「NEED NOT(しなくてよい)」という用語は, 刊行物の範囲において, 行動指針が許容できることを示す. 

「CAN(できる)」及び「CANNOT(できない)」という用語は, 物質的, 物理的, 偶発的であろうとなかろうと, 可能性や能力があること, または否定の意味ではその可能性や能力が欠如していることを意味する. 


<!--
The terms "SHALL" and "SHALL NOT" indicate requirements to be followed strictly in order to conform to the publication and from which no deviation is permitted.

The terms "SHOULD" and "SHOULD NOT" indicate that among several possibilities one is recommended as particularly suitable, without mentioning or excluding others, or that a certain course of action is preferred but not necessarily required, or that (in the negative form) a certain possibility or course of action is discouraged but not prohibited.

The terms "MAY" and "NEED NOT" indicate a course of action permissible within the limits of the publication.

The terms "CAN" and "CANNOT" indicate a possibility or capability, whether material, physical or causal or, in the negative, the absence of that possibility or capability.
-->

<div class="breaker"/>

<div class="text-center" markdown="1">
## Table of Contents
</div>

[1. 目的](#sec1)

[2. はじめに](#sec2)

[3. 定義及び略語](#sec3)

[4. Authenticator Assurance Levels](#sec4)

[5. Authenticator及びVerifierの要件](#sec5)

[6. Authenticatorライフサイクルの要件](#sec6)

[7. セッション管理](#sec7)

[8. 脅威とセキュリティに関する考慮事項](#sec8)

[9. プライバシに関する考慮事項](#sec9)

[10. ユーザビリティに関する考慮事項](#sec10)

[11. 参照](#references)

[付録A &mdash; 記憶シークレットの強度](#appA)

<!--
[1. Purpose](#sec1)

[2. Introduction](#sec2)

[3. Definitions and Abbreviations](#sec3)

[4. Authenticator Assurance Levels](#sec4)

[5. Authenticator and Verifier Requirements](#sec5)

[6. Authenticator Lifecycle Requirements](#sec6)

[7. Session Management](#sec7)

[8. Threats and Security Considerations](#sec8)

[9. Privacy Considerations](#sec9)

[10. Usability Considerations](#sec10)

[11. References](#references)

[Appendix A &mdash; Strength of Memorized Secrets](#appA)
-->
