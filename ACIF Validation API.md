![](https://drive.google.com/uc?id=1MStOYYaZDqrvuOwlmecX0iayL0Jt_eAN)

# ACIF Validation API 

## About this document 

This API spec was initially drafted by Daniel Brackett of Extreme Reach and donated to IAB Tech Lab for further development by the [Advanced TV Commit Group](https://iabtechlab.com/working-groups/advanced-tv-commit-group/) to support Tech Lab’s Ad Creative ID Framework (ACIF). 

Please contact support@iabtechlab.com if you have any questions or comments about this document. This document and other related resources can be found on the IAB Tech Lab website at: [https://iabtechlab.com](https://iabtechlab.com)

### IAB Tech Lab Lead: 
Katie Stroud, Senior Product Manager 

### About IAB Tech Lab 

The IAB Technology Laboratory (Tech Lab) is a non-profit consortium that engages a member community globally to develop foundational technology and standards that enable growth and trust in the digital media ecosystem. Comprised of digital publishers, ad technology firms, agencies, marketers, and other member companies, IAB Tech Lab focuses on improving the digital advertising supply chain, measurement, and consumer experiences, while promoting responsible use of data. Its work includes the Open Real-Time Bidding (OpenRTB) bidding protocol, ads.txt anti-fraud specification, Open Measurement SDK for viewability and verification, Video Ad Serving Template (VAST), Global Privacy Platform (GPP), and other for a growing suite of products to support advertising technology. Established in 2014, the IAB Tech Lab is headquartered in New York City with staff located remotely across the US and abroad. 

### Disclaimer 

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TARDE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE. 

### License 

F/RAND which means fair, reasonable, and non-discriminatory terms, denoting “a voluntary licensing commitment that standards organizations often request from the owner of an intellectual property right (usually a patent) that is, or may become, essential to practice a technical standard. Put differently, a F/RAND commitment is a voluntary agreement between the standard-setting organization and the holder of standard-essential patents." ~[Wikipedia](https://en.wikipedia.org/wiki/Reasonable_and_non-discriminatory_licensing)

## Table of Contents

- [Executive Summary](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#executive-summary)
  - [Audience](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#audience)
    - [Ad Registration Authorities](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#ad-registration-authorities)
    - [Ad Technology Platforms](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#ad-technology-platforms)
- [About ACIF](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#about-acif)
- [API Overview](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#api-overview)
  - [Terminology](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#terminology)
  - [API Components](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#api-components)
    - [Ad Registries](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#ad-registries)
    - [Globally Unique Ad Creative Identifiers](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#globally-unique-ad-creative-identifiers)
    - [UniversalAdId Validation](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#universaladid-validation)
    -[ Ad registration for ads with multiple creative ](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#ad-registration-for-ads-with-multiple-creative)
- [The Validation Request](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#the-validation-request)
  - [Where to Find the UniversalAdId](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#where-to-find-the-universaladid)
  - [About the UniversalAdId in VAST](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#about-the-universaladid-in-vast)
  - [When and Where to Send a Validation Request](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#when-and-where-to-send-a-validation-request)
  - [URL Character Escaping](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#url-character-escaping)
  - [UniversalAddId Validation](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#universaladid-validation-1)
  - [Open Validation with HEAD Request](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#open-validation-with-head-request)
- [The Validation Response](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#the-validation-response)
  - [Object: UniversalAdId](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#object-universaladid)
  - [Object: Relationship](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#object-relationship)
  - [Error Codes](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#error-codes)
- [Testing Sandbox](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#testing-sandbox)
- [Implementation Over Existing APIs](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#implementation-over-existing-apis)
- [Examples](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#examples)
  - [UniversalAdId Validation](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#universaladid-validation-2)
  - [Open UniversalAdId Validation](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#open-universaladid-validation)
  - [Validation of Unknown UniversalAdId](https://github.com/InteractiveAdvertisingBureau/ACIF/blob/main/ACIF%20Validation%20API.md#validation-of-unknown-universaladid)

## Executive Summary 

As part of the Ad Creative ID Framework (ACIF), the ACIF Validation API specification defines requests to named ad registries for validating ads registered within the named registry using the assigned unique ID. 

ACIF was designed to increase ad registration for ad creative in campaigns set up to run in CTV and other TV-like video environments. A key benefit of ad registration is leveraging the assigned unique IDs to validate the ad’s registration status for ad decisioning, measurement, and creative reconciliation. This ACIF Validation API automates validation, resulting in an open ecosystem whereby multiple ad registries can interoperate, instead of relying on proprietary API semantics and metadata schemas. The API also supports the retrieval of metadata associated with the ad creative, which can then be used for ad decisioning such as frequency capping, competitive separation, and brand suitability. 

Many ad registries already have an API that supports this function, but implementing the ACIF Validation API standardizes validation and creates interoperability that scales the benefits that ACIF offers. This scale supports growth in CTV inventory and innovation in the products offered to buyers. 

To bring this scale and growth to the market, ad registration authorities need to implement support for this API. Ad technology platforms can use this API to integrate with participating ad registries. 

## Audience 

In general, anyone in the CTV and video supply chain who works directly with ad creative as part of campaign set up, execution, and reporting should be familiar with ACIF and at least aware that the ACIF Validation API is being used to validate ad creative for ad decisioning, measurement, and creative reconciliation.. 

Beyond the general audience, developers and certain ad ops professionals in the ad tech and ad registration organizations should use this document in the following ways: 

### Ad Registration Authorities 

Developers should use the specifications outlined in this document to make adjustments in their existing API for validation, or to build one if the registry currently does not support validation by API. 

### Ad Technology Platforms 

Developers should use the specifications outlined in this document to integrate their ad receiving and/or ad measurement technology with ad registration authorities to automate ad validation and metadata requests. Beyond validation, developers can also use the validated ID in their decisioning algorithms and reporting operations. 

## About ACIF 

Ad Creative ID Framework (ACIF) encourages buyers to register their ads with market registration authorities, and supply the assigned unique identifiers as part of the metadata for their ads. The ad technology businesses, publishers, and other parties along the way are also encouraged to validate these unique identifiers (UniversalAdId), and leverage them in their ad decisioning algorithms, measurement, and creative reconciliation. 

The framework is patterned loosely after the Internet Domain Name System (DNS). Just as DNS depends on a clear system for uniqueness of resources to promote Internet interoperability, the advertising supply chain needs a clear system for uniquely identifying ads. ACIF is that system. 

The goal of ACIF is to ensure global uniqueness of identifiers across registries. The ACIF Validation API promotes interoperability between parties in the ecosystem so that campaign execution and reporting can be performed with greater accuracy and efficiency. 

## API Overview 

The ACIF Validation API is an HTTP request from a technology party to an ad registry that signals whether a provided unique ID exists in the registry’s system. A registered ad, in the digital supply chain, should supply a unique ID along with the root domain of the registry that issued the ID. Together, these two pieces of metadata represent a UniversalAdId–a term first introduced with the release of [VAST 4](https://iabtechlab.com/standards/vast/). Given the root domain of the ad registry, the requesting party has the needed information on where to send the request for validation. This information can be looked up in the ACIF Directory in [IAB Tech Lab’s Tool Portal](https://tools.iabtechlab.com/transparencycenter/explorer/business/creativeid). For more information on the ACIF Directory, review the ACIF documentation under the section, “ACIF Directory.” 

Once validated, the ad registry returns a minimum set of metadata to define the Advertiser, Brand, Language, and Duration. Ad registries may provide additional metadata at their discretion upon request. Ask your ad registry partners about additional metadata they may provide and how to access it. 

### Terminology 

The following terms are used throughout this document specifically in the context of ACIF and this specification. 
  
|Term |	Definition |
|---|---|
|Universal Ad Identifier (UniversalAdId) |	A globally unique ad identification code, issued by a recognized Ad Registry, that distinguishes a specific ad creative, specified variations if applicable, and certain metadata about the ad. |
|Ad Registry |	A regional ad registration authority that maintains records for ad creative as entered by the ad’s owner, typically a brand, or a representative of the owner. Upon registration, the ad is assigned a unique identifier (UniversalAdId). |
|ACIF Directory |	A central listing of ACIF-compliant ad registries, maintained in [IAB Tech Lab Tools Portal](https://tools.iabtechlab.com/home).| 
|Validation API User |	Makes the request to the ad registry using ad platform algorithms to validate a UniversalAdId and receive metadata about the validated asset. |
|Ad Metadata |	A set of attributes stored within an ad registry and associated with a creative asset as identified by a UniversalAdId. |

### API Components 

The following points define the basic components underlying the ACIF Validation API, some of its basic rules, and its evolution. 

#### Ad Registries 

A core principle of the framework is the designation of Ad Registries that are recognized suppliers of durable, unique creative identifiers within the advertising creative ecosystem. The list of recognized Ad Registries is maintained by IAB Tech Lab in the [Tools Portal](https://tools.iabtechlab.com/home). Each listed ad registry is responsible for the following primary functions: 

- Providing the means for brands (or a second party acting on the brand’s behalf) to register their ad creative and assigning a unique identifier to each creative submitted for registration. All assigned IDs must be unique within the registry. 
- Enabling third party access to validate ads that have been assigned a unique ID by the registry. At a minimum, ad registries should allow any system to receive a true/false response to a validation request. 
- Providing a minimum set of required metadata to approved users as outlined below:
  - **Advertiser**: Typically the business that owns the brand or product represented in the ad.
  - **Brand**: The suite of products or services represented in the ad. The product name could also be represented here.
  - **Language**: The spoken or written language used in the ad.
  - **Duration**: The length of the ad in seconds. A duration of “0” indicates a static image. 

Registries may require authentication for access to the above metadata. IAB Tech Lab and the Advanced TV Commit Group recommend allowing easy access that fosters adoption while maintaining the registries’ policies and commitment to their customers. Removing barriers to access, as much as business practices allow, increases ad registration and enables interested parties to experience the benefits of cross-platform asset identification. 

Additional metadata may be provided at the discretion of the ad registry according to its policies. Parties wishing to access additional metadata must reach out to the registry for their protocol on such access. An authenticated account, subscription, or other arrangements may be necessary. 

#### Globally Unique Ad Creative Identifiers 

Another important component of the Framework is distinguishing the ID of one ad registry from the IDs issued by other registries. Each issued ID must be unique within the registry, and to avoid any duplication from other registries, parties submitting the issued ID for validation must also supply the root domain of the issuing registry. This additional metadata acts as a name space for issued IDs, ensuring that they are universally unique, even if two or more registries issue the same UniversalAdId value. This is similar to the “top level domain” (TLD) used with Internet domains (e.g. .com, .org, .edu, etc.), and informs validation parties on which registry to check. 

- The combination of the <mark>ad registry root domain</mark>  + <mark>registry-issued creative ID</mark> must be globally unique. Together, these two pieces of information represent the UniversalAdId introduced in Tech Lab’s Video Ad Serving Template v4 (VAST 4) and central to ACIF. 

#### UniversalAdId Validation 

The final component of the Framework is support for *standardized validation*. Any UniversalAdId can be validated according to the mechanisms offered by each registry. However, these mechanisms have been proprietary and not always automated. 

The ACIF Validation API standardizes how a UniversalAdId is validated and automates the process across platforms. Implementation enables parties throughout the marketing supply chain to easily confirm the uniqueness and source for creative identifiers without having to implement custom registry integrations. 

- UniversalAdId validation is supported by calling the validation API endpoint using the HTTP GET method. If the UniversalAdId is successfully validated by the named ad registry then a 200 OK response is returned, with a standard metadata schema. Otherwise, a 404 Not Found is returned. 
- The validation operation may or may not require authentication by the caller, depending on the requirements of the ad registry and their contractual arrangements with clients. 
- Regardless of authentication, all participating registries provide an open validation mechanism, accessed by clients by calling the validation API endpoint using the HTTP HEAD method. If the UniversalAdId is successfully validated by the issuing registry then a ‘204 No Content’ empty response is returned (with no metadata). Otherwise, a ‘404 Not Found’ response is returned. 

#### Ad registration for ads with multiple creative 

- Ad registration should result in an issued ID for every base ad creative. Ad registries may offer a system or hierarchy to issue sub-IDs for variants and complementary creative. The resulting UniversalAdId should be used for messaging specific to that creative, regardless of where the ad serves. For example, a video ad creative used across linear TV, CTV, web and social channels should use the same UniversalAdId for all usages and video transcodings to ensure that data from various sources can be aligned to the same creative message. 
- Relationships between 2 or more UniversalAdIds may be expressed to indicate parent-child associations, aliases, derivatives, or format translations. This can be done with the relationship object specified and allows for UniversalAdId "graphs" to be established that promote discovery and interoperability. 
- Dynamic creative optimization (DCO) for creative may produce hundreds or thousands of variants by localizing information such as weather, store locations, or other compartmentalized details. For DCO ads, only the base creative needs to be registered. DCO is currently unsupported in this version of the ACIF Validation API; however, for buyers that want data on the multiple variants, discuss your options with your ad registry and any campaign partners. 

## The Validation Request 

Validation in this API is implemented using a REST API operation that follows a standard URI request and response format. The request is made using a URL provided by the registration authority appended with the ID to be validated. A HEAD request can also be used for a simple response that returns either a 404 Not Found (ID doesn’t exist) or a 204 OK/301 Redirect (ID exists). 

### Where to Find the UniversalAdId 

The UniversalAdId is the ID assigned when an ad is registered and includes the domain of the registry that issued the ID. This information should be expected as part of the metadata for any ads sent for placement–typically in a VAST response. Other sources may provide this information as part of any campaign set-up. Ask your customers and your partners to provide valid, registered IDs along with the domain of the registration authority, and agree on how and when the information is supplied. 

### About the UniversalAdId in VAST 

In December 2022, VAST CTV Addendum 2024 was released to enable backwards compatibility for all VAST versions to include a <UniversalAdId> for each creative in a VAST tag (along with other features introduced in VAST 4.0+ for use in serving advanced video). The placement of the <UniversalAdId> node is specified for each version in the Addendum. Please place registered IDs in your tags as specified. Publishers and ad tech vendors will look for the UniversalAdId according to spec in this Addendum. 

### When and Where to Send a Validation Request 

A simple HTTP HEAD request can be sent at any time a UniversalAdId is encountered. See **Open Validation with HEAD Request** below for details. To receive metadata as part of the validation, a request is made to the registration authority using a URL as posted in the ACIF Directory. 

To find the validation URLs for listed registries, login IAB Tech Lab Tools Portal (sign up is free) and navigate to the list of registries as part of the Data Explorer for Businesses. Here you can see which ad registration authorities participate in ACIF and whether they support the ACIF Validation API. 

For a deeper level of validation that includes a response with metadata, the same URL is used, but you may need to create an account with the registration authority. With credentials for authentication built into your validation process, you can receive metadata and use it as allowed by your agreement with the registration authority. Ideally, it allows for using metadata for ad decisioning, measurement, and enabling creative reconciliation. 

**Note**: Validation requests should only be made for new ad creative. Once called, the validation and metadata should be cached to avoid subsequent pulls on the same ad. More efficient methods may be developed over time, but for this initial version, validation occurs with a request for each new ad. 

### URL Character Escaping 

For HTTP requests that include the UniversalAdId in the URL path or query string, the UniversalAdId value must be URL-escaped to encode any reserved non-alphanumeric characters, such as colon, forward slash, etc. For example, a validation GET operation for the UniversalAdId code “ABC/12345/030” would be escaped as https://acif.example.com/uaids/ABC%2F12345%2F030.

### UniversalAdId Validation 

Access to core ad creative metadata is another important feature of the ACIF framework. The metadata associated with a UniversalAdId is accessed using the HTTP GET method. 

|Operation |	Verb |	Description |	Return Type |
|---|---|---|---|
|/uaids/{creative_identifier} |	GET |	Verifies a submitted, URL-escaped creative_dentifier as being a UniversalAdId that was issued by the Ad Registry and returns the verified UniversalAdId object and associated metadata.** |	UniversalAdId, 404 Not Found or 301 Redirect (see Error Codes) |

### Open Validation with HEAD Request 

Ad registries may require authentication for validation and retrieval of metadata according to their current policies and user agreements. However, when authentication is not required, at least for basic validation, a head request may be used to validate a UniversalAdId. 

|Operation |	Verb |	Description |	Return Type |
|---|---|---|---|
|/uaids/{creative_identifier} |	HEAD |	Verifies a submitted, URL-escaped creative_dentifier as being a UniversalAdId that was issued by the Ad Registry |	204 No Content, 404 Not Found or 301 Redirect (see Error Codes) |

## The Validation Response 

The payload structures for the API response objects are simple JSON data structures that carry a small number of attributes. 

An optional attribute may have a default value to be assumed if omitted. If no default is indicated, then by convention its absence should be interpreted as *unknown*. Empty strings or null values should be interpreted the same as omitted (i.e., the default if one is specified or *unknown* otherwise). 

Note: As a convention in this document, objects being defined are denoted with uppercase first letter in deference to the common convention for class names in programming languages such as Java, whereas actual instances of objects and references thereto in payloads are lowercase. 

### Object: UniversalAdId 

The UniversalAdId object represents a unique ad identifier created for a client by an ad registry. The ad registry sends the following UniversalAdId object in response to a request for ID validation. The request is detailed 

|Attribute |	Type |	Definition |
|---|---|---|
|universalAdId | string (required) |	Globally unique ad identifier code that includes the root domain of the issuing registry + the issued ID. This is the same value used in the request. |
|arUri |	string (required) |	The fully qualified URI that returns this UniversalAdId from the issuing ad registry. This is the same value used to make the request. |
|advertiser |	string (required) |	The advertiser associated with the creative identified by the UniversalAdId |
|brand |	string (required) |	The brand associated with the creative identified by UniversalAdId. Advertiser hierarchies can be complex and “brand” can mean different things for different advertisers. This field is intended to name the product represented in the ad. |
|duration |	number (required) |	The duration (in seconds) of the creative identified by the UniversalAdId (for static content, such as display ad units, a duration of 0 is used) |
|language |	string (required) |	The primary ISO language of the creative identified by the UniversalAdId (e.g. en, fr, de, etc.) |
|owner |	string (optional) |	The name of the client organization/entity that paid for the UniversalAdId |
|product |	string (optional) |	The product associated with the creative identified by the UniversalAdId |
|creativeType | String (Optional) |	The primary mime-type category of the creative identified by the UniversalAdId (e.g. video, audio, image, text, etc.). Please reference syntax on mime-types. |
|relationships | Array of Relationship objects (Optional) |	The list of creative identifiers (ACIF-compliant or other) that this UniversalAdId is related to. Values for this field help to define generated versions of the original ad creative. Please see Object: Relationship below for details on what is returned when this attribute is supported. |
|validationCode	| Custom (Optional) |	A custom field to support regional codes that indicate an asset has been cleared for placement. Use of this field is critical in some markets where a code or set of codes define how an ad can be placed. For example, in the UK, Clearcast may issue codes for an asset that is safe for children’s programming. The data returned may be a string, a structured object, or even a Boolean value. Discuss the use of this field with the registration authorities that you work with. |

### Object: Relationship 

The Relationship object represents a secondary identifier that is related to the UniversalAdId of a base ad. When optionally included in a metadata response, it allows for the expression of various types of relationships, such as a parent, child, sibling or alias. 

The alias relationship allows a UniversalAdId to be linked to other creative identifiers, such as legacy codes, house numbers, watermarks, fingerprints, etc. The parent, child and sibling relationships can be used to indicate hierarchies or associations with different versions of a creative. 

When the identifier specified in a Relationship is another UniversalAdId, then the corresponding uri property would be the fully qualified ad registry validation API URL that returns the associated ad metadata. If the identifier represents a non-ACIF identifier, then the uri property would hold the URL to return the associated object representation (if available). 

The relationship construct provides a very flexible means of associating other identifiers, objects and metadata sets with a UniversalAdId. 

|Attribute |	Type |	Definition |
|---|---|---|
|identifier |	string; required |	Related creative identifier. For example, the secondary ID for a variant of the base ad creative. |
|type |	string; required |	One of the following: 'Parent', 'Child', 'Sibling' or 'Alias' (see description in the text above this table) |
|uri |	string 	(Optional)| A fully qualified URI that returns a representation of the object referenced by the identifier |

### Error Codes 

When a valid response cannot be returned, standardized HTTP status codes may be returned as follows. 

```javascript
{
error: “error type”,
message: “detailed explanation” 
} 
```

| Error |	Message |
|---|---|
|400 Bad Request | Malformed input. |
|401 Unauthorized |	Missing or invalid token. |
|403 Forbidden	| Insufficient access. | 
|404 Not Found |	Unknown creative identifier. |
|500 Internal Server Error |	Unexpected server error. |
|301 Moved Permanently |	Redirect to external registry. |
|429 Too Many Requests |	Rate limit exceeded. |

## Testing Sandbox 

Each listed registry in the ACIF program may provide a testing sandbox and a test ID to enable ad tech platforms to test their implementation of the ACIF Validation API. The URL for this testing sandbox, if provided, is listed for the registry in the Tech Lab Tools Portal. 

## Implementation Over Existing APIs 

Ideally all ad registries listed as part of the ACIF program will build their validation API to this spec and ad tech companies wishing to use the ACIF Validation API will make the adjustments in their systems to support. However, many ad tech companies may already be working with a registry’s existing API. Transition will take time, but this standardized API offers new opportunities to improve existing APIs and enable a more interoperable system for creative asset management. 

Updates to support the new API may require some adjustments, and over time, the benefits of this standardized API will enable new functions that were not possible before. 

## Examples 

For documentation purposes, the references and examples below use the Ad Registry hostname https://acif.example.com. 

### UniversalAdId Validation 

Following is an example of a standard validation operation for a registered UniversalAdId. 

```javascript
  Request:  GET https://acif.example.com/ucids/ACME000123
  Authorization: {optional-authentication-token}
  Response: 200 OK
  Payload:
  {
    "UniversalAdId": "adregistry.com.ACME000123H",
    "uri": "https://acif.example.com/uaids/ACME000123",
    "advertiser": "Acme",
    "brand": "Coyote Tools",
    "owner": "Acme International",
    "product": "Invisible Paint",
    "creativeType": "video",
    "duration": "30",
    "language": "en"
    "relationships": []
} 
```

### Open UniversalAdId Validation 

Following is an example of an open (non-authenticated) validation operation for a registered UniversalAdId. 

```javascript 
  Request:  HEAD https://ucif.example.com/uaids/ACME000123
  Response: 204 No Content
  Payload: [empty]
```

### Validation of Unknown UniversalAdId 

The following is an example of a UCID verification operation where an identifier not issued by the ad registry was passed in the request. 

```javascript 
  Request:  GET https://ucif.example.com/uaids/UNKOWNID000
  Response: 404 Not Found
```

