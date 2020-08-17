# Handy cheat sheet

### 1. [HTML] Validating a nth-digit number

    <input id="phone" type="text" name="phone" 
        maxlength="10" pattern="[0-9]{10}" 
        title="Please enter exactly 10 digits" required>

That will check for an integer (0-9) values with a maximum of 10 digits.


### 2. [HTML] Validating an email to require .{any_string} at the end

The "email" type on HTML only checks for an @ sign with any values on the end but does not consider the dot (.) before the domain extension (e.g. myemail@test.com).

This pattern will also check to require .{any_string} with a minimum of 2 characters at the end

    <input id="email" type="email" name="email"
        pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
        title="Please enter a valid email" required>

### 3. [JS] Comparing JavaScript objects

I've searched a lot on this one but finally I got the most simple solution that worked on what I'm trying to achieve.

I just converted a JavaScript object or value to a JSON string and that's it:

    return JSON.stringify(baseObject) === JSON.stringify(comparedObject);
