Asymmetrik FHIR API Server + Mongo Example
==========================================
[![Build Status](https://travis-ci.org/Asymmetrik/node-fhir-server-mongo.svg?branch=master)](https://travis-ci.org/Asymmetrik/node-fhir-server-mongo)
[![Known Vulnerabilities](https://snyk.io/test/github/asymmetrik/node-fhir-server-mongo/badge.svg?targetFile=package.json)](https://snyk.io/test/github/asymmetrik/node-fhir-server-mongo?targetFile=package.json)

## Intro
This project is an example project built on `@asymmetrik/node-fhir-server-core` and has a MongoDB back end storing sample data. It's built with the ability to run in docker or node.js. To get started developing in Docker, see [Getting Started with Docker](#getting-started-with-docker). To get started developing with Node.js and Mongo, see [Getting Started with Node](#getting-started-with-node).  You can serve multiple versions of FHIR with just one server.  By default, DSTU2 (1.0.2) and STU3 (3.0.1) is enabled.  You can choose to support both versions or just one version by editing the config.

## Getting Started with Docker

1. Install the latest [Docker Community Edition](https://www.docker.com/community-edition) for your OS if you do not already have it installed.
2. Run `docker-compose up`.

## Getting Started with Node

1. Install the latest LTS for [Node.js](https://nodejs.org/en/) if you do not already have it installed.
2. Install the latest [Mongo Community Edition](https://docs.mongodb.com/manual/administration/install-community/) if you do not already have it installed.
3. Make sure the default values defined in `env.json` are valid.
4. Run `yarn` or `npm install`.
5. Run `yarn start` or `npm run start`.

## Next Steps
The server should now be up and running on the default port 3000. You should see the following output:

```shell
... - verbose: Server is up and running!
```

### Lets give this a try on your server

#### Capability Statements
By default, both DSTU2 and STU3 is enabled for the Patient and Observation resource.  The capability statements are dynamically generated based on which resources you enable.
 - View the DSTU2 Conformance Statement [http://localhost:3000/1_0_2/metadata](http://localhost:3000/1_0_2/metadata)
 - View the STU3 Capability Statement [http://localhost:3000/3_0_1/metadata](http://localhost:3000/3_0_1/metadata)

Using any request builder (i.e. Postman), let's create a new patient.

#### STU3 Patient (Content-Type: application/fhir+json)
```
Create Patient

PUT /3_0_1/Patient/hhPTufqen3Qp-997382 HTTP/1.1
Host: localhost:3000
Content-Type: application/fhir+json
Cache-Control: no-cache

# Raw Body
{
  "resourceType" : "Patient",
  "id" : "hhPTufqen3Qp-997382",
  "text" : {
    "status" : "generated",
    "div" : "<div xmlns=\"http://www.w3.org/1999/xhtml\"><table><tbody><tr><td>Name</td><td>Peter James <b>Chalmers</b> (&quot;Jim&quot;)</td></tr><tr><td>Address</td><td>534 Erewhon, Pleasantville, Vic, 3999</td></tr><tr><td>Contacts</td><td>Home: unknown. Work: (03) 5555 6473</td></tr><tr><td>Id</td><td>MRN: 12345 (Acme Healthcare)</td></tr></tbody></table>    </div>"
  },
  "identifier" : [ {
    "use" : "usual",
    "type" : {
      "coding" : [ {
        "system" : "http://hl7.org/fhir/v2/0203",
        "code" : "MR"
      } ]
    },
    "system" : "urn:oid:1.2.36.146.595.217.0.1",
    "value" : "hhPTufqen3Qp997382",
    "period" : {
      "start" : "2001-05-06"
    },
    "assigner" : {
      "display" : "Acme Healthcare"
    }
  } ],
  "active" : true,
  "name" : [ {
    "use" : "official",
    "family" : "Smith",
    "given" : [ "Peter", "James" ]
  }, {
    "use" : "usual",
    "given" : [ "Jim" ]
  } ],
  "telecom" : [ {
    "use" : "home"
  }, {
    "system" : "phone",
    "value" : "(07) 7296 7296",
    "use" : "work"
  } ],
  "gender" : "male",
  "birthDate" : "1974-12-25",
  "deceasedBoolean" : false,
  "address" : [ {
    "use" : "home",
    "line" : [ "255 Somewhere Rd" ],
    "city" : "Pleasant Valley",
    "state" : "Somewhere",
    "postalCode" : "3999"
  } ],
  "contact" : [ {
    "relationship" : [ {
      "coding" : [ {
        "system" : "http://hl7.org/fhir/v2/0131",
        "code" : "CP"
      } ]
    } ],
    "name" : {
      "family" : "Smith",
      "given" : [ "Jane" ]
    },
    "telecom" : [ {
      "system" : "phone",
      "value" : "+33 (237) 123456"
    } ],
    "gender" : "female",
    "period" : {
      "start" : "2012"
    }
  } ],
  "managingOrganization" : {
    "reference" : "Organization/hhPTufqen3Qp-997382-RZq1u"
  }
}

```

```
Read Patient

GET /3_0_1/Patient/hhPTufqen3Qp-997382 HTTP/1.1
Host: localhost:3000
Content-Type: application/fhir+json
Cache-Control: no-cache

```



#### DSTU2 Patient (Content-Type: application/json+fhir)
```
Create Patient

PUT /1_0_2/Patient/12345997382 HTTP/1.1
Host: localhost:3000
Content-Type: application/json+fhir
Cache-Control: no-cache

# Raw Body
{
  "resourceType" : "Patient",
  "id" : "12345997382",
  "text" : {
    "status" : "generated",
    "div" : "<div><table><tbody><tr><td>Name</td><td>Peter James <b>Chalmers</b> (&quot;Jim&quot;)</td></tr><tr><td>Address</td><td>534 Erewhon, Pleasantville, Vic, 3999</td></tr><tr><td>Contacts</td><td>Home: unknown. Work: (03) 5555 6473</td></tr><tr><td>Id</td><td>MRN: 12345 (Acme Healthcare)</td></tr></tbody></table>    </div>"
  },
  "identifier" : [ {
    "use" : "usual",
    "type" : {
      "coding" : [ {
        "system" : "http://hl7.org/fhir/v2/0203",
        "code" : "MR"
      } ]
    },
    "system" : "urn:oid:1.2.36.146.595.217.0.1",
    "value" : "12345997382",
    "period" : {
      "start" : "2001-05-06"
    },
    "assigner" : {
      "display" : "Acme Healthcare"
    }
  } ],
  "active" : true,
  "name" : [ {
    "use" : "official",
    "family" : [ "Chalmers" ],
    "given" : [ "Peter", "James" ]
  }, {
    "use" : "usual",
    "given" : [ "Jim" ]
  } ],
  "telecom" : [ {
    "use" : "home"
  }, {
    "system" : "phone",
    "value" : "(07) 7296 7296",
    "use" : "work"
  } ],
  "gender" : "male",
  "birthDate" : "1974-12-25",
  "deceasedBoolean" : false,
  "address" : [ {
    "use" : "home",
    "line" : [ "255 Erewhon St" ],
    "city" : "PleasantVille",
    "state" : "Vic",
    "postalCode" : "3999"
  } ],
  "contact" : [ {
    "relationship" : [ {
      "coding" : [ {
        "system" : "http://hl7.org/fhir/patient-contact-relationship",
        "code" : "partner"
      } ]
    } ],
    "name" : {
      "family" : [ "du", "Marché" ],
      "given" : [ "Bénédicte" ]
    },
    "telecom" : [ {
      "system" : "phone",
      "value" : "+33 (237) 123456"
    } ],
    "gender" : "female",
    "period" : {
      "start" : "2012"
    }
  } ],
  "managingOrganization" : {
    "reference" : "Organization/1"
  }
}
```

```
Read Patient

GET /1_0_2/Patient/12345997382 HTTP/1.1
Host: localhost:3000
Content-Type: application/json+fhir;charset=UTF-8
Cache-Control: no-cache

```

### Determine which resources you want to support
In this example, only the Patient and Organization resource is filled out.  You will need to fill in the other services for the resources you would like to support.  The routes will only be available for the resource you enabled. You can view the available resources over at [`@asymmetrik/node-fhir-server-core`](https://github.com/Asymmetrik/node-fhir-server-core#profiles).

## License
`@asymmetrik/fhir-server-mongo` is [MIT licensed](./LICENSE).
