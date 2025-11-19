# OpenFGA-AuthZEN-Auth0-Google-Zanzibar
Modern Authorization Implementation with OpenID AuthZEN and OpenFGA

A Globally Distributed Authorization System - https://www.zanzibar.academy/

The business situation
# OpenFGA Authorization Model for Global Corporation

## Identity Structure Overview

This document outlines the authorization model for a large corporation operating across hundreds of global markets using OpenFGA.

### Hierarchy Levels

#### 1. Global Level (Corporation)

The **Global** entity serves as the master identity with the following roles:

- **Global Director**
  - Owns all system documents
  - Has editing rights over documents from any market or restaurant

- **Global Manager**
  - Can view every document in the system
  - Cannot edit any documents regardless of market or restaurant

- **Global Workforce Employee**
  - No default access to any system documents
  - Cannot view or edit anything without explicit authorization

#### 2. Market Level (Countries/Regions)

**Markets** represent individual countries or regions (e.g., France, USA) with the following roles:

- **Market Director**
  - Can own and edit all documents within their specific market and its restaurants
  - Has no authority over documents outside their market
  - Example: A France director cannot modify US documents

- **Market Manager**
  - Has viewing rights only for documents within their assigned market and its restaurants
  - No access outside their area
  - Example: A France manager cannot see US documents

- **Market Workforce Employee**
  - Lacks permission to view or edit any documents related to restaurants or the market by default

#### 3. Restaurant Level

- **Franchisee**
  - Responsible for all documents within their own restaurant
  - Can edit these documents
  - Cannot access documents from other restaurants

- **Restaurant Manager**
  - May view any document pertaining solely to their restaurant
  - No access to documents from other restaurants

- **Crew Members**
  - Do not have permission to view any documents by default
  - No access to their own restaurant or elsewhere in the system

### Authorization Requirements

Employees who need access to a document must get approval from their respective Director through the appropriate channel—corporation, market, or restaurant.

## Document Access Rules

### Restaurant Documents
- Can only be accessed by authorized personnel from:
  - The specific restaurant
  - The parent market
  - The corporation

### Market Documents
- Accessible solely to approved individuals within that specific market or the corporation
- Example: A French market document is available to authorized French employees, but not to US employees

### Corporate-level Documents
- Restricted to authorized individuals at the corporate level only
- Not accessible by staff in markets or restaurants

## Tuple Management

### User Types
- `user:id` (individual user)
- `object:id#relation` (inherited relation)
- `object:*` (wildcard)

### Employee Directory

| Name     | Employee ID | Function                                    |
|----------|-------------|---------------------------------------------|
| Wei      | ID9920      | Global Director                             |
| Adrien   | ID24817     | Global Manager                              |
| Megan    | ID1991      | Global Employee                             |
| Damien   | ID11444     | France Director                             |
| Edouard  | ID23205     | France Manager                              |
| Mathieu  | ID20896     | France Employee                             |
| Valerie  | ID37143     | US Director                                 |
| Kyle     | ID2137      | US Manager                                  |
| Carrie   | ID34530     | US Employee                                 |
| Andrew   | ID11283     | US Franchisee – Restaurant ID 005           |
| Peter    | ID570       | US Franchisee – Restaurant ID 006           |
| Anna     | ID12725     | US Franchisee – Restaurant ID 007           |
| Paola    | ID19892     | US Manager - Restaurant ID 005              |
| Sofia    | ID23878     | US Crew - Restaurant ID 005                 |
| Victoria | ID12208     | US Manager – Restaurant ID 006              |
| Leon     | ID23736     | US Crew – Restaurant ID 006                 |
| Patricia | ID11810     | France Franchisee – Restaurant ID 001       |
| Paul     | ID37409     | France Manager - Restaurant ID 001          |
| Patrick  | ID2901      | France Crew - Restaurant ID 001             |

### Document Inventory

| Doc ID   | Function                                    |
|----------|---------------------------------------------|
| Doc23398 | Invoice for Restaurant ID 001 in France     |
| Doc36053 | Invoice for Restaurant ID 001 in France     |
| Doc2175  | Invoice for Restaurant ID 005 in US         |
| Doc12281 | Invoice for Restaurant ID 007 in US         |
| Doc42830 | Invoice for Restaurant ID 007 in US         |
| Doc3956  | Invoice for Restaurant ID 006 in US         |
| Doc40875 | Training Material for France Market         |
| Doc13973 | Training Material for US Market             |
| Doc9334  | Training Material for Global employee       |

---

## Next Steps

Once the authorization model is implemented in OpenFGA, tuples need to be created mapping:
- **User** (employee IDs)
- **Object** (document IDs, market IDs, restaurant IDs)
- **Relation** (owner, editor, viewer, etc.)
  
# Bibliography
- [Modelling ReBAC Access Control System with Ontologies and Graph Databases](https://artem-goncharov.medium.com/modelling-rebac-access-control-system-with-ontologies-and-graph-databases-1ddab8b8bcf4)
- [How to Protect Your API with OpenFGA: From ReBAC Concepts to Practical Usage](https://dev.to/this-is-learning/how-to-protect-your-api-with-openfga-from-rebac-concepts-to-practical-usage-4n9j)
- [Langchain, OpenFGA and python](https://github.com/auth0-samples/auth0-ai-samples/tree/main/authorization-for-rag/langchain-python)
- [Building a Secure RAG with Python, LangChain, and OpenFGA](https://auth0.com/blog/fine-grained-access-control-with-python-flask/)
- [A Developer's Guide to Fine-Grained Authorization (FGA)](https://www.youtube.com/watch?v=5ethvBQqRkg)
- [Modern Authorization Implementation with OpenID AuthZEN and OpenFGA](https://www.youtube.com/watch?v=Klps-Crhwmo)
