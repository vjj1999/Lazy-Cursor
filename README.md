# Awesome Backend Development Rules 🚀

> A guide showcasing backend development best practices and their evolution, based on real project experience

## Project Migration Guide 🔄

To adapt these guidelines for your project:

1. In COMPOSER, enter the following text:
```
View <project_guidelines> tags in .cursorrules. Replace the <project_guidelines> tags in .cursorrules according to the project structure and the corresponding Unified Middleware. The content of the tags is required to meet the needs of the workflow and strictly express the project guidelines.
```

2. This will generate customized project guidelines based on your specific project structure and middleware requirements.

## Project Structure 📁

```
.
├── api/            # API documentation and Swagger files
├── controller/     # HTTP handlers
├── logic/         # Business logic
├── repository/    
│   ├── dto/      # Request objects
│   ├── vo/       # Response objects
│   └── model/    # Database models
├── services/      
│   ├── xxx_service/  # Complex business services
│   └── xxx/         # Utility services
├── middleware/    # Global middleware
├── third_party/  # Third-party integrations
├── constant/
│   └── errcode/  # Error codes
├── tests/        # Test files
├── util/         # Utility functions
└── scripts/      # Database migration scripts
```

## Layer Standards Evolution 🏗️

### Controller Layer

```go
// Controller standards
func (ctrl *UserController) Create(c *gin.Context) {
    // Use application.TraceCtx(ctx)
    ctx := application.TraceCtx(c.Request.Context())
    
    // Validate input with ShouldBind
    var req dto.CreateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        return echo.Error(c, errcode.InvalidParams, err)
    }
    
    // Call logic layer
    user, err := ctrl.logic.CreateUser(ctx, req)
    if err != nil {
        return echo.Error(c, err)
    }
    
    return echo.Success(c, user)
}
```

### Logic Layer

```go
// Logic standards
func (l *UserLogic) CreateUser(ctx context.Context, req dto.CreateUserRequest) (*vo.UserVO, error) {
    // Business validation
    if err := l.validateUser(ctx, req); err != nil {
        return nil, errs.NewBusinessErr(errs.ValidationFailed, err.Error())
    }
    
    // Transaction handling
    tx := model.BeginCtxTx(ctx)
    defer tx.Rollback()
    
    // Create user
    user, err := l.userRepo.Create(ctx, req.ToModel())
    if err != nil {
        return nil, err
    }
    
    if err := tx.Commit(); err != nil {
        return nil, err
    }
    
    return vo.FromUser(user), nil
}
```

### Service Layer

```go
// Service standards
type UserService struct {
    Ctx context.Context
    repo UserRepository
}

func NewUserService(ctx context.Context, repo UserRepository) *UserService {
    return &UserService{
        Ctx: ctx,
        repo: repo,
    }
}

func (s *UserService) Create(ctx context.Context, user *model.User) error {
    // Domain logic with proper error handling
    if err := s.validateUserDomain(user); err != nil {
        return errs.NewBusinessErr(errs.ValidationFailed, err.Error())
    }
    
    return s.repo.Create(ctx, user)
}
```

## Logging Standards 📝

```go
// Structured logging with proper context
func (s *Service) ProcessOrder(ctx context.Context, order *Order) error {
    // Error level
    if err := s.validate(order); err != nil {
        cdslog.W(ctx).Error("order validation failed",
            zap.String("order_id", order.ID),
            zap.Error(err))
        return err
    }
    
    // Info level
    cdslog.W(ctx).Info("processing order",
        zap.String("order_id", order.ID),
        zap.String("status", order.Status))
        
    // Debug level
    cdslog.W(ctx).Debug("order details",
        zap.Any("order", order))
        
    return nil
}
```

## Testing Evolution 🧪

```go
// Integration test with test containers
func TestIntegration_UserFlow(t *testing.T) {
    // Setup test containers
    postgres, err := testcontainers.NewPostgresContainer()
    require.NoError(t, err)
    defer postgres.Terminate(context.Background())
    
    // Initialize test application
    app := NewTestApplication(postgres.GetDSN())
    
    // Test cases
    tests := []struct {
        name    string
        request dto.CreateUserRequest
        want    int
    }{
        {
            name: "valid user creation",
            request: dto.CreateUserRequest{
                Email: "test@example.com",
            },
            want: http.StatusOK,
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            resp := app.CreateUser(tt.request)
            assert.Equal(t, tt.want, resp.Code)
        })
    }
}
```

## Error Handling Standards ⚠️

```go
// Error definition
var (
    ErrUserNotFound = errs.NewBusinessErr(40001, "user not found")
    ErrInvalidInput = errs.NewBusinessErr(40002, "invalid input parameters")
)

// Error handling in service
func (s *Service) GetUser(ctx context.Context, id string) (*User, error) {
    user, err := s.repo.Find(ctx, id)
    if err != nil {
        if errors.Is(err, sql.ErrNoRows) {
            return nil, ErrUserNotFound
        }
        // Log error with trace ID
        cdslog.W(ctx).Error("failed to find user",
            zap.String("user_id", id),
            zap.Error(err))
        return nil, err
    }
    return user, nil
}

// Standardized error response
type ErrorResponse struct {
    Code    int         `json:"code"`
    Message string      `json:"message"`
    Data    interface{} `json:"data,omitempty"`
}
```

## Continuous Improvement 🔄

Our guidelines continue to evolve with:
- New technology stack best practices
- Performance optimization patterns
- Security measures
- Architectural solutions
- Testing coverage requirements
- CI/CD pipeline improvements

Remember to regularly check .cursorrules for the latest standards and update your implementation accordingly.
