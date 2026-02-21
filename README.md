# Hanzo IAM Go SDK

Go client SDK for [Hanzo IAM](https://hanzo.ai), providing authentication, authorization, and identity management.

## Installation

```bash
go get github.com/hanzoid/go-sdk@latest
```

## Quick Start

```go
import "github.com/hanzoid/go-sdk/iam"

func main() {
    iam.InitConfig(
        "https://id.hanzo.ai",   // endpoint
        "your-client-id",        // clientId
        "your-client-secret",    // clientSecret
        jwtPublicKey,            // certificate
        "your-org",              // organizationName
        "your-app",              // applicationName
    )

    users, err := iam.GetUsers()
    if err != nil {
        panic(err)
    }
    fmt.Println(users)
}
```

## Configuration

| Parameter        | Required | Description                                            |
|-----------------|----------|--------------------------------------------------------|
| endpoint         | Yes      | IAM server URL (e.g., `https://id.hanzo.ai`)          |
| clientId         | Yes      | Application client ID                                   |
| clientSecret     | Yes      | Application client secret                                |
| certificate      | Yes      | JWT public key (PEM format)                              |
| organizationName | Yes      | Organization name                                        |
| applicationName  | Yes      | Application name                                         |

## Multi-Client Usage

```go
client1 := iam.NewClient(endpoint, clientId, clientSecret, certificate, orgName, appName)
client2 := iam.NewClient(endpoint2, clientId2, clientSecret2, certificate2, orgName2, appName2)
```

## OAuth Authentication

```go
// Get token from authorization code
token, err := iam.GetOAuthToken(code, state)

// Parse JWT claims
claims, err := iam.ParseJwtToken(token.AccessToken)

// Refresh token
newToken, err := iam.RefreshOAuthToken(refreshToken)
```

## User Management

```go
users, err := iam.GetUsers()
user, err := iam.GetUser("username")
user, err := iam.GetUserByEmail("user@example.com")

user := &iam.User{
    Owner:       "org-name",
    Name:        "john_doe",
    DisplayName: "John Doe",
    Email:       "john@example.com",
}
success, err := iam.AddUser(user)
success, err := iam.UpdateUser(user)
success, err := iam.DeleteUser(user)
```

## Authorization

```go
allowed, err := iam.Enforce("user", "resource", "action")
```

## Resources

The SDK supports: Users, Organizations, Applications, Roles, Permissions, Providers, Tokens, Sessions, Certificates, Resources, Webhooks, Emails, SMS, Syncers, Plans, Pricings, Subscriptions, Transactions, Orders, Payments, Groups, Adapters, Enforcers, Models, Invitations, and LDAP.

## License

Apache-2.0
