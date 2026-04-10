# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   **TypeScript:**
   ```typescript
   // Testable
   function processOrder(order, paymentGateway) {}

   // Hard to test
   function processOrder(order) {
     const gateway = new StripeGateway();
   }
   ```

   **C#:**
   ```csharp
   // Testable
   void ProcessOrder(Order order, IPaymentGateway paymentGateway) {}

   // Hard to test
   void ProcessOrder(Order order) {
     var gateway = new StripeGateway();
   }
   ```

2. **Return results, don't produce side effects**

   **TypeScript:**
   ```typescript
   // Testable
   function calculateDiscount(cart): Discount {}

   // Hard to test
   function applyDiscount(cart): void {
     cart.total -= discount;
   }
   ```

   **C#:**
   ```csharp
   // Testable
   Discount CalculateDiscount(Cart cart) {}

   // Hard to test
   void ApplyDiscount(Cart cart) {
     cart.Total -= discount;
   }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup
