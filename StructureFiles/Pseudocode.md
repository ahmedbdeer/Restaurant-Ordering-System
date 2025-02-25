# Pseudocode for Cart Management Processes

This document contains pseudocode for two key processes in a restaurant ordering system: **Add to Cart** and **Modify Cart**. Each section includes the pseudocode along with detailed explanations of each step.

---

## Pseudocode 1: Add to Cart

The **Add to Cart** process ensures that a user can add an item to their shopping cart. The process checks if the user is logged in, displays the item details, and then adds the selected item to the cart. If the item is already in the cart, its quantity is incremented.

```plaintext
BEGIN AddToCartProcess
    // Step 1: Check if user is logged in
    IF NOT is_logged_in THEN
        DISPLAY "Please log in or register."
        TRIGGER login_or_registration()
    END IF

    // Step 2: Display item details
    DISPLAY item_details

    // Step 3: User clicks "Add to Cart"
    ON_CLICK "Add to Cart" DO
        // Check for active cart
        IF user_cart IS NULL THEN
            CREATE new_cart
            SET user_cart = new_cart
        END IF

        // Check if item exists in cart
        item_exists = FALSE
        FOR EACH item IN user_cart.items DO
            IF item.id == selected_item.id THEN
                item.quantity += 1  // Increment quantity
                item_exists = TRUE
                BREAK
            END IF
        END FOR

        // If item not found, add to cart
        IF NOT item_exists THEN
            ADD selected_item TO user_cart.items WITH quantity = 1
        END IF

        // Display updated cart
        DISPLAY user_cart
        PROMPT "Proceed to checkout or continue browsing?"
    END ON_CLICK
END
## Pseudocode 2: Modify Cart
```plaintext
BEGIN ModifyCartProcess
    // Step 1: User opens cart page
    DISPLAY cart_page WITH user_cart.items

    // Step 2: User selects item to modify
    selected_item = GET_INPUT("Select item (by ID or name): ")

    // Step 3: Choose action (Update or Remove)
    DISPLAY "Choose action: [1] Update Quantity, [2] Remove Item"
    action = GET_INPUT("Enter action (1 or 2): ")

    CASE action OF
        "1":  // Update Quantity
            new_quantity = GET_INPUT("Enter new quantity: ")
            IF new_quantity > 0 THEN
                UPDATE selected_item.quantity TO new_quantity
            ELSE
                REMOVE selected_item FROM user_cart.items
            END IF

        "2":  // Remove Item
            REMOVE selected_item FROM user_cart.items

        DEFAULT:
            DISPLAY "Invalid action."
    END CASE

    // Refresh and display updated cart
    DISPLAY user_cart
END
