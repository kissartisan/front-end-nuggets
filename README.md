# Handy cheat sheet

### 1. Validating a 10-digit number using only HTML

Define a mutator in your model (most likely app\User.php) which would encrypt all your password fields:

    <input id="phone" type="text" name="phone" maxlength="10" pattern="[0-9]{10}" title="Please enter exactly 10 digits" required>

That will check for an integer (0-9) values with a maximum of 10 digits.
