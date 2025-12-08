# project_rules
Adding file with project for clean project


1. Core Architecture Rules

Follow MVC + Service + Repository pattern.

Strict separation of concerns:

Routes → define endpoints only.

Controllers → receive request, validate, call service.

Services → business logic.

Repositories → database operations.

Models → schema only.

No module should depend on files outside its layer.

2. File Size & Function Size Rules

Max 80 lines per file.

Max 10 lines per function.

If content exceeds the limit → split automatically into smaller files.

Controllers should be 5–10 lines max.

3. Folder Structure Rules

Your backend must always follow this structure:

src/
  routes/
    user/
      userRoutes.js
  controllers/
    user/
      signupController.js
      loginController.js
      verifyOtpController.js
      forgotPasswordController.js
      resetPasswordController.js
  services/
    user/
      signupService.js
      loginService.js
      verifyOtpService.js
      forgotPasswordService.js
      resetPasswordService.js
  repositories/
    user/
      userRepository.js
  models/
    userModel.js
  validators/
    user/
      signupValidator.js
      loginValidator.js
  middlewares/
    authMiddleware.js
  utils/
    hashPassword.js
    comparePassword.js
    generateToken.js
    sendEmail.js

4. Routing Rules

Routes must ONLY map endpoints → controllers.

No logic allowed inside route files.

Each domain (user, product, order, etc) must have its own route folder.

Example:

router.post("/signup", signupController);
router.post("/login", loginController);

5. Controller Rules

Controllers must:

Be 5–10 lines.

Handle request + response only.

Call a service.

Never contain logic.

Never contain database queries.

Always use try/catch and return JSON.

Controller responsibilities
✔ Validate input
✔ Call service
✔ Return response
❌ No business logic
❌ No DB queries

6. Service Rules

Services:

Contain the actual business logic.

Max 20–25 lines (then split).

Must NOT return Express response, only data/objects.

Cannot access req/res directly.

Should call repositories for DB operations.

Examples of services:

create user

login user

send OTP

verify OTP

reset password

update profile

7. Repository Rules

Repositories:

Handle all database operations.

Must interact only with Mongoose Models.

Cannot validate input.

Cannot perform business logic.

Example responsibilities:

find user by email

create user

update user

delete user

8. MongoDB / Mongoose Rules

Models define schema only.

No logic inside models except virtuals/hooks if necessary.

No mixed schema + business code.

Use repository pattern for:

.find()

.create()

.updateOne()

.deleteOne()

9. Validation Rules

All input validation must be in validator files.

Never validate inside controllers/services.

Use Joi, Yup, or custom logic.

Example:

signupValidator.js
loginValidator.js
updateProfileValidator.js

10. Naming Rules

File names must reflect exact responsibility:
✔ signupController.js
✔ signupService.js
✔ userRepository.js
❌ main.js
❌ userUtils.js

Names must be descriptive and meaningful.

11. API Response Rules

Always return:

{
  success: true/false,
  message: "",
  data: {...}
}


No HTML responses.
No raw text responses.

12. Security Rules

Always hash passwords (bcrypt or argon2).

Never return passwords or tokens.

Use:

Helmet

CORS

Rate limit

Validation

Sanitization

Environment variables must be loaded from .env.

13. Error Handling Rules

Services must throw errors.

Controllers must catch errors.

Errors must be returned in standard JSON format:

{
  success: false,
  message: error.message
}

14. Middleware Rules

All auth logic must be in /middlewares.

Middlewares should be < 15 lines.

No business logic inside middleware.

Middleware should always call next().

15. Code Generation Rules for AI

When generating code:

AI must follow these hard rules

Maximum 10 lines per function.

Maximum 80 lines per file.

Automatically split logic across multiple:

controllers

services

repositories

validators

utils

Must NOT place multiple features in one file.

Must follow folder structure rules strictly.

Must always produce clean, modular, MVC-compliant code.

AI must avoid:

❌ Big controller files
❌ Multiple endpoints in same controller
❌ Mixing controller + service + DB in one file
❌ Long functions
❌ Business logic inside controllers
❌ Multilevel nested if/else

16. Example Workflow (AI Must Follow)

When asked to “add signup API”, AI should automatically create:

signupController.js
signupService.js
signupValidator.js
userRepository.js (reuse)


When asked to “add login API”, AI should create:

loginController.js
loginService.js
loginValidator.js


When asked to “add product module”, AI should create a full folder:

controllers/product/
services/product/
repositories/product/
validators/product/
routes/product/

17. General Clean Code Principles

Single Responsibility Principle (SRP)

No duplicated code

Reusable helpers

Small functions

Clear naming

Modular architecture

Consistent formatting
