# aicode-rules

1. It focuses on the specific tech stack and patterns used:
- Gin framework
- RabbitMQ
- Redis
- PostgreSQL
- Zap logger
- JWT auth

2. It matches the actual architectural layers:
- controller/
- logic/
- service/
- repository/

3. It emphasizes actual patterns seen in the code:
- Context usage
- Error handling with errs.NewBusinessErr
- Echo response formatting
- Queue message structures
- Transaction management

4. It includes project-specific concerns:
- OSS integration
- Payment processing
- User subscription handling
- Credit system
- Digital person management

The rules now better reflect the actual practices and patterns used in the codebase rather than generic backend concepts.
