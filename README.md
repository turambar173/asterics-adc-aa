# Technologies for Authentication and Authorization in an Astronomical Data Center

Softwares and technologies to manage A&A in an astronomical data center must satisfy a number of requirements. In particular they must allow:

- access to private and public data according to data policy
- data sharing among users
- access to software and computational resources according to data policy
- data computing through workflow applications
 

Softwares and technologies described in this section have been used in the IA2 Data Center, which is is an Italian Astrophysical research infrastructure service of INAF that manages astronomical data archives, mainly for ground-based telescopes (LBT, TNG, etc.), also allowing data computing through workflow applications.

The following table collects system requirements and main features of the technologies described in details below.

<table><tbody><tr><td>
<strong>Technology</strong>
</td>
<td>
<strong>System Requirements</strong>
</td>
<td>
<strong>Main Features</strong>
</td>
</tr><tr><td>
SAML2.0
</td>
<td>
<ul>
<li>Deployment of IdP and SP</li>
<li>Authentication method</span></li>
</ul>
</td>
<td>
<p>Common XML-based open-standard to exchange authentication and authorisation data to address Web SSO issues. It can deal with any authentication method.</p>
</td>
</tr><tr><td>
SimpleSAMLphp
</td>
<td>
<ul>
<li>PHP version &gt;= 5.3.0</li>
<li>Apache &gt;= 2.2</li>
</ul>
</td>
<td>
Lightweight open-source application that deals with authentication. Easy to configure, it supports several identity protocols and framework.
</td>
</tr><tr><td>
Grouper
</td>
<td>
<ul>
<li>Java &gt;= 7</li>
<li>Tomcat &gt;= 6</li>
<li>A RDBMS supported by Hibernate</li>
</ul>
</td>
<td>
<p>An enterprise access management system able to retrieve user information from multiple sources. It provides a web user interface, web services and an administration shell.</p>
</td>
</tr></tbody></table>


## SAML2.0

The Security Assertion Markup Language (SAML) standard defines a framework for exchanging authentication and authorization data between parties, in particular, between an IdP and a SP. SAML2.0 is a version of the SAML standard ratified in March 2005.

In a typical SAML use case there are three roles: the principal (the user), the IdP and the SP. The principal requests a service from the SP, e.g. the user requests access to a web resource provided by the SP. The SP requests and obtains an identity assertion from the IdP, typically the SP redirect the user to the IdP for authentication and the IdP returns to the SP an identity assertion. On the basis of this assertion, the SP can make an access control decision, i.e. it can decide whether to authorise the access to the requested resource to the user or not.

SAML does not specify the method of authentication at the IdP, which can be anything. SAML is only responsible of the security data exchange between IdP and SP.


## SimpleSAMLphp

SimpleSAMLphp is an open source lightweight implementation of several federation protocols written in PHP that deals with authentication. The main focus of SimpleSAMLphp is providing support for:

- SAML 2.0 as a Service Provider (SP)
- SAML 2.0 as an Identity Provider (IdP)

However, it also supports some other identity protocols and frameworks, such as Shibboleth 1.3, A-Select, CAS, OpenID, WS-Federation or OAuth. For more details about SimpleSAMLphp you can check the website https://simplesamlphp.org.

We used SimpleSAMLphp for

- deploying the IdP
- deploying the SP
- configuring the federation between the IdP and the SP
- managing the exchange of identity assertions between the IdP and the SP


## Grouper
## 
Grouper is an enterprise access management system designed for the highly distributed management environment and heterogeneous information technology environment. It is written in Java and provides web services access, a user friendly web interface and an administration shell.

We used Grouper for managing user groups defining access rights on astronomical archive protected resources.

Grouper is able to retrieve user information from multiple sources (like LDAP or other databases). It is also possible to add external subjects (users whose information are not stored in any of the configured sources).

Groups can be created by the administrator, manually, using the UI, or executing a script in the GrouperShell, or via the web services (both SOAP and REST). Groups can be organized in folders, called stems.

Users and groups information are stored into a relational database, called registry. This database is created by Grouper itself during the first setup.

For each user inside a group it is possible to define a very fine range of permissions:

- ADMIN: can assign access privileges and manage all group information;
- UPDATE: can manage membership of the group;
- READ: can see the membership of the group;
- VIEW: can see the group;
- GROUP_ATTR_READ: can read attributes assigned to the group;
- GROUP_ATTR_UPDATE: can assign attributes to the group;
- OPTIN: can add self to the membership;
- OPTOUT: can remove self from membership.
 

So, setting proper grants, it is possible to configure an user to be able to add other users in groups he or she is managing. This possibility allowed to let principal investigators manage their co-investigators accesses, avoiding the administrator has to perform this kind of tasks too.

External applications can call the Grouper web services for retrieving authorization information about users that want to access protected resources. Java applications can also access these services using the provided API.

For more details about Grouper you can check the [Grouper Official Website](https://www.internet2.edu/products-services/trust-identity/grouper/).
