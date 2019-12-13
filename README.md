# Push-Button-Door-VHDL-
Simulation of a push button door lock with a variable password.


**Design Strategy : Block Diagram **

![Block Diagram](https://github.com/shahjui2000/Push-Button-Door-VHDL-/blob/master/el_strategy.jpg)


**Modules:**

1.Keypad Scanner
2.Decoder (Decoding which key is pressed from input row and column
3.Debouncer( For taking care of multiple pressing of a single key)
4.Store Module (For Password Reset)
5.Lock-Unlock state module (Main Logic of Push-Button Door)
6.Display: Shown by LED or a bit(0 or 1 for Locked and Unlocked states respectively)

**FSM : Lock and Unlock Logic of Door**

![FSM1](https://github.com/shahjui2000/Push-Button-Door-VHDL-/blob/master/EL_FSM.jpg)

1.S1 state is reached when a key is pressed and then it move S2, S3 and S4 which are wait states and goes to S5 whenever Kd and K are both 1. If Kd and K are both 1 early on, they skip to S5 state directly. This procedure of using wait states, K and Kd is Debouncing which helps us to process each key entered by user efficiently. Kd is nothing but K delayed by two clock cycles and is implemented by using 2 consecutive D-flip flops. 

2.Once, the state S5 is reached, the key pressed is stored in a vector and count is incremented. Count helps us keep an idea of the  number of keys entered since our application deals with variable password of length 4 to 7.

3.If # is entered after password is inputted, inserted password is checked with the stored password and if they match, the door enters unlocked state and remains there until # is kept pressed. AS soon as # is released, door enters locked state. If the password is incorrect, the user has to enter password again.

4.If a * is pressed after password is entered and if it is correct, then store mode is entered wherein the user needs to enter a new password 2 time,s of 4 to 7 length(we know a password is terminated when user enters #). If both times inserted password match each other then password is reset. If not, user has to enter new password again twice.

5.Reset Button is present, which if pressed; leds straight to store mode instead of first entering the old password followed by *.

**FSM : Store Mode(Password Changing Mode)**

![FSM2](https://github.com/shahjui2000/Push-Button-Door-VHDL-/blob/master/fsm_2.png)


**References:**

Digital systems design using VHDL-C.Roth

https://vhdlwhiz.com/std_logic_vector/

https://www.fpga4student.com/2017/09/vhdl-code-for-seven-segment-display.html

https://www.nandland.com/vhdl/examples/example-variable.html
