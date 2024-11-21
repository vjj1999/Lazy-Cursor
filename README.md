# Awesome Backend Development Rules 🚀

> A guide showcasing backend development best practices and their evolution, based on real project experience

## Why These Rules? 🤔

In real development, we often face these challenges:
- Inconsistent code structure
- Chaotic error handling
- Unclear business logic layering
- Difficult project maintenance

This ruleset demonstrates how we solve these problems step by step.

## Technology Stack Evolution 📚

### Gin Framework Selection Journey

**Initial Problem:**
```go
// Issues with direct net/http usage
http.HandleFunc("/api/user", func(w http.ResponseWriter, r *http.Request) {
    // Repetitive routing logic
    // Difficult middleware management
    // Cumbersome parameter validation
})
```

**Solution:**
```go
// Improvements with Gin framework
r := gin.Default()
r.POST("/api/user", func(c *gin.Context) {
    // Unified middleware
    // Convenient parameter binding
    // Standardized error handling
})
```

### Message Queue Integration (RabbitMQ)

**Evolution Process:**
1. Initial Direct Processing
```go
// Synchronous processing causing response delays
func ProcessOrder(order Order) {
    // Direct order processing
    // Send email
    // Update inventory
}
```

2. After Queue Integration
```go
// Improved performance with async processing
func ProcessOrder(order Order) {
    // Send to message queue
    rabbitmq.Publish("orders", order)
}

func OrderConsumer() {
    // Async order processing logic
}
```

## Architectural Layer Practices 🏗️

### Why This Layering?

Showing evolution from chaos to clarity:

**Early Code:**
```go
// All logic mixed together
func HandleUser(c *gin.Context) {
    // Parameter validation
    // Business logic
    // Database operations
    // Error handling
    // Response return
}
```

**After Layering:**
```go
// Controller Layer - HTTP Request Handling
func (ctrl *UserController) Create(c *gin.Context) {
    var req CreateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        return
    }
    user, err := ctrl.logic.CreateUser(req)
    // ...
}

// Logic Layer - Business Logic
func (l *UserLogic) CreateUser(req CreateUserRequest) (*User, error) {
    // Business rule validation
    // Multiple service calls
}

// Service Layer - Domain Services
func (s *UserService) Create(user *User) error {
    // Single domain logic
}

// Repository Layer - Data Access
func (r *UserRepository) Create(user *User) error {
    // Database operations
}
```

## Testing Evolution 🧪

### Unit Testing Journey

**Initial Approach:**
```go
// Basic test without mocks
func TestCreateUser(t *testing.T) {
    user := CreateUser("test@example.com")
    if user.Email != "test@example.com" {
        t.Error("email not set correctly")
    }
}
```

**Evolved Testing Practice:**
```go
// Using test tables and mocks
func TestUserService_Create(t *testing.T) {
    tests := []struct {
        name    string
        input   CreateUserRequest
        mock    func(*MockRepo)
        wantErr bool
    }{
        {
            name: "successful creation",
            input: CreateUserRequest{
                Email: "test@example.com",
            },
            mock: func(m *MockRepo) {
                m.EXPECT().
                    Create(gomock.Any()).
                    Return(nil)
            },
            wantErr: false,
        },
        // More test cases...
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            // Test implementation
        })
    }
}
```

### Integration Testing Framework

```go
// Integration test setup
func TestIntegration_UserFlow(t *testing.T) {
    // Use test containers for dependencies
    postgres, err := testcontainers.NewPostgresContainer()
    if err != nil {
        t.Fatal(err)
    }
    defer postgres.Terminate(context.Background())

    // Test full flow
    app := NewTestApplication(postgres.GetDSN())
    response := app.CreateUser(CreateUserRequest{
        Email: "test@example.com",
    })
    
    assert.Equal(t, http.StatusOK, response.Code)
}
```

### Mock Strategies

```go
// Interface-based mocking
type UserRepository interface {
    Create(context.Context, *User) error
    Find(context.Context, string) (*User, error)
}

// Mock implementation
type MockUserRepository struct {
    mock.Mock
}

func (m *MockUserRepository) Create(ctx context.Context, user *User) error {
    args := m.Called(ctx, user)
    return args.Error(0)
}
```

## Error Handling Evolution ⚠️

```go
// Early error handling
if err != nil {
    c.JSON(500, gin.H{"error": err.Error()})
    return
}

// Improved business error handling
if err != nil {
    return errs.NewBusinessErr(errs.UserNotFound, "user not found")
}

// Standardized error response
{
    "code": 40001,
    "message": "user not found",
    "data": null
}
```

## Project-Specific Practices 🌟

### OSS Integration
```go
// Evolution from simple upload to complete file management
type OSSService interface {
    UploadFile(ctx context.Context, file *File) (*FileInfo, error)
    GetSignedURL(ctx context.Context, objectKey string) (string, error)
    // ...
}
```

### Payment System Evolution
```go
// Modular payment system design
type PaymentService interface {
    // Support multiple payment channels
    CreateOrder(ctx context.Context, req *CreateOrderRequest) (*Order, error)
    ProcessCallback(ctx context.Context, params map[string]string) error
}
```

## Continuous Improvement 🔄

Our ruleset continues to evolve with the project:
- New tech stack best practices
- Performance optimization experiences
- Security measures
- New feature architectural solutions
- Testing coverage requirements
- CI/CD pipeline improvements
