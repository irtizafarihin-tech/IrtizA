# Crisp & Sizzle Kiosk

Choose a combo, decide whether to upsize, and let the kiosk apply any student
rebate. It will show the total and calculate your change after you pay.

## How the kiosk works

```text
START

    DISPLAY "Welcome to Crisp & Sizzle! What would you like today?"
    DISPLAY "1. Chicken Combo - RM12.00"
    DISPLAY "2. Burger Combo - RM10.00"
    DISPLAY "3. Veggie Wrap Combo - RM8.00"
    DISPLAY "4. Cancel & Exit"

    INPUT MenuOption

    // Match the customer's choice to a meal and its price.
    IF MenuOption = 1 THEN
        MealName = "Chicken Combo"
        MealPrice = 12.00
    ELSE IF MenuOption = 2 THEN
        MealName = "Burger Combo"
        MealPrice = 10.00
    ELSE IF MenuOption = 3 THEN
        MealName = "Veggie Wrap Combo"
        MealPrice = 8.00
    ELSE IF MenuOption = 4 THEN
        DISPLAY "Transaction Cancelled"
    ELSE
        DISPLAY "Invalid Choice!"
    END IF

    // Only continue with an order when a meal was selected.
    IF MenuOption = 1 OR MenuOption = 2 OR MenuOption = 3 THEN
        DISPLAY "Would you like to upsize for RM2.00? (YES or NO)"
        INPUT UpsizeChoice

        IF UpsizeChoice = "YES" THEN
            Upsize = 2.00
        ELSE
            Upsize = 0.00
        END IF

        Subtotal = MealPrice + Upsize

        DISPLAY "Are you a student? (YES or NO)"
        INPUT StudentStatus

        IF StudentStatus = "YES" THEN
            Rebate = Subtotal * 0.10
        ELSE
            Rebate = 0.00
        END IF

        FinalTotal = Subtotal - Rebate

        DISPLAY "Here's your order:"
        DISPLAY "Meal: ", MealName
        DISPLAY "Upsize: RM", Upsize
        DISPLAY "Student rebate: RM", Rebate
        DISPLAY "Total to pay: RM", FinalTotal

        DISPLAY "Please enter your cash amount:"
        INPUT CashAmount

        IF CashAmount >= FinalTotal THEN
            Change = CashAmount - FinalTotal
            DISPLAY "Payment successful. Thanks for your order!"
            DISPLAY "Your change: RM", Change
        ELSE
            DISPLAY "Sorry, that's not enough to cover the total."
            DISPLAY "Your order has been cancelled."
        END IF
    END IF

STOP
```
