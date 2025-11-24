
***

# Integration API Inventory

**Date Generated:** November 24, 2025
**Purpose:** Compliance and Technical Auditing
**Scope:** MoneyGuard SDK, Linkage Assurance Integration, and Wimika Demo Bank.

---

## 1. MoneyGuard Service APIs
These APIs are used by the Mobile SDK for core MoneyGuard functionality including claims, policy management, and behavioral biometrics.

*   **Base URL:** `https://moneyguardrestservice-ephgezbka5ggf7cb.uksouth-01.azurewebsites.net`
*   **Authentication:** Bearer Token (Authorization Header)

### Claims
| Method | Endpoint | Function Name | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v2/claim` | `submitClaims` | Submits a new claim. Payload is `multipart/form-data` including attachments. |
| `GET` | `/api/v1/claim` | `getClaims` | Retrieves a list of claims. Supports filtering by date range, bank, and status. |
| `GET` | `/api/v1/claim/{id}` | `getClaim` | Retrieves details of a specific claim by ID. |
| `GET` | `/api/v1/claim/incident-values` | `getIncidentNames` | Retrieves a list of valid incident type names. |

### Policy & Coverage
| Method | Endpoint | Function Name | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/v1/coveragelimit` | `getCoverageLimits` | Retrieves available coverage limits. |
| `GET` | `/api/v1/policyoption` | `getPolicyOptions` | Retrieves policy options based on a selected coverage limit ID. |
| `GET` | `/api/v2/userbankaccounts` | `getUserAccounts` | Retrieves bank accounts associated with the user for a specific partner bank. |
| `POST` | `/api/v2/policy` | `createPolicy` | Creates a new insurance policy for the user. |
| `GET` | `/api/v1/policy/coverage-for-sdk` | `getCoverageForSdk` | Retrieves active coverage details specifically formatted for the SDK. |
| `GET` | `/api/v1/policy/by-bank-id` | `getUserPolicyByBankId` | Retrieves policy details associated with the current bank ID. |

### Authentication & Security
| Method | Endpoint | Function Name | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/session` | `login` | Initiates a session. |
| `POST` | `/api/v1/credential/check` | `checkCredentials` | Validates user credentials. |
| `POST` | `/api/v1/trusted-device/trust/{deviceId}` | `trustDevice` | Registers a device as a trusted device. |
| `POST` | `/api/v1/transaction/debit-check` | `debitCheck` | Validates if a debit transaction is safe/allowed. |

### Biometrics (Typing Profile)
| Method | Endpoint | Function Name | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/biometric/match-typing-profile` | `matchTypingProfile` | Compares current typing behavior against stored profile. |
| `POST` | `/api/v1/biometric/save-typing-profile` | `saveTypingProfile` | Captures and saves a new typing profile. |
| `POST` | `/api/v1/biometric/verify-typing-profile` | `verifyTypingProfile` | Verifies a user based on typing profile. |
| `POST` | `/api/v1/biometric/save-typing-profile-auth` | `saveTypingProfileAuth` | Saves a typing profile during an authenticated session. |
| `POST` | `/api/v1/biometric/verify-typing-profile-auth` | `verifyTypingProfileAuth` | Verifies a typing profile during an authenticated session. |
| `GET` | `/api/v1/biometric/is-typing-pattern-enrolled` | `isEnrolled` | Checks if a specific typing pattern type is already enrolled. |

### Content
| Method | Endpoint | Function Name | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/mobile/in-app-content` | `getInAppContent` | Retrieves dynamic content for the mobile application. |

---

## 2. Linkage Assurance Insurance APIs
These APIs interface with the legacy `ies_connect.php` gateway. Routing is handled via query parameters (`process` and `process_code`) rather than distinct URL paths.

*   **Base URL:** `https://ies.linkageassurance.com/demo/gen_api/ies_connect.php`
*   **Authentication:** Bearer Token + PHPSESSID Cookie

### Underwriting
| Method | Process Name | Process Code | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `Processopenledapi` | `102` | **Get Policy:** Retrieval of existing policy details. |
| `POST` | `Processopenledapi` | `102` | **Create Policy:** Creation of a new policy record. |
| `POST` | `Processopenledapi` | `100` | **Create Client:** Registers a new insured client/customer. |
| `GET` | `Processopenledapi` | `104` | **Get Client's Policy:** Look up policy by Client Number. |
| `GET` | `Processopenledapi` | `114` | **Get Client:** Retrieve client personal details. |
| `POST` | `Processopenledapi` | `922` | **Policy Renewal:** Renew an existing policy (Transaction Type: RNL). |

### Claims
| Method | Process Name | Process Code | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `GetPolicyPeriod` | N/A | **Get Policy Period:** Check validity period for a policy number. |
| `GET` | `DebitNote` | N/A | **Get Billings:** Retrieve Debit Note information. |
| `POST` | `Processopenledapi` | `944` | **Save Claims:** Register a new claim incident. |
| `GET` | `Processopenledapi` | `108` | **Get Claim:** Retrieve details of a specific claim number. |

### Miscellaneous / Utilities
| Method | Process Name | Process Code | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `Processopenledapi` | `945` | **Get Policy Document:** Generates/Retrieves the PDF policy document. |
| `GET` | `Processopenledapi` | `946` | **Get Available Endorsement:** Checks for available endorsements on a policy. |
| `GET` | `Processopenledapi` | `947` | **Get Reinsurance Setup:** Retrieves reinsurance configuration for the current year. |

---

## 3. Wimika Demo Bank APIs
APIs used to simulate banking operations for the demo application.

*   **Base URL:** `{{baseUrl}}` (Configurable environment variable)
*   **Headers:** `x-alumnihub-session-id`, `x-wimika-session-id`, or `x-wimika-partner-token`

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/BankAccount` | Retrieves a collection of the user's bank accounts. |
| `POST` | `/api/BankAccount` | Creates a new bank account. |
| `GET` | `/api/BankAccount/{id}` | Retrieves details of a specific bank account. |
| `POST` | `/api/Debit` | Performs a general debit operation with security context (typing patterns). |
| `POST` | `/api/DebitTransaction` | Records a specific debit transaction between accounts. |
| `POST` | `/api/Deposit` | Performs a deposit operation, supporting attachment uploads. |
| `GET` | `/api/Session` | Retrieves a user session based on a partner token. |
| `GET` | `/api/Transaction` | Retrieves a history of user transactions. |
| `GET` | `/api/Transaction/{id}` | Retrieves details of a specific transaction. |
