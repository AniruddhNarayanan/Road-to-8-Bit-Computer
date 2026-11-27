# Checkpoint 1: 8-Bit Addition:

## As of 11/26/2026, I have completed a fully functional 8-Bit Adder circuit. 

### Documentation:

My first main setback was when i was trying to make a full adder. I had previously already figured out how to make a full adder a few months ago, and all that I remembered was that it needed 4 logic gates if it needed to support adding a carry to the sum result of A and B (I later realized that I needed 5 so trying to limit myself to the 4 that I remembered was something I was doing wrong). So to figure out which logic gates were needed I drew out the truth tables on my iPad, with a column for A, B, C, O2, and O1. In this truth table O1 represnted the first output bit which is equal to 1, and O2 representing the second output bit.
| Input A | Input B | Input C (Carry) | Output 2 (Carry Out) | Output 1 (Sum) |
|:---:|:---:|:---:|:---:|:---:|
| 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 | 1 |
| 1 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 |
---

 After drawing out the truth table I realized O1 would only be TRUE under 2 conditions.
  1. If only 1 out of the 3 inputs A, B, or C were active, or
  2. If all three of the inputs were active.

From the first point I realized I would need an XOR gate that checks all 3 of the inputs. This is because an 2 input XOR gate only outputs when only 1 of the inputs are true, and i would also need a AND gate to detect when all 3 are displaying as true. Since all gates in Logisim as far as I know is only able to handle two inputs, so having both the XOR and the AND gate to determine the result of O1 needing 3 gates was a challenge. However, I realized after some playing around that having an XOR of A XOR B output into the input of an XOR that also gets the input of C would be the same as having a 3 input XOR for A, B, and C. 

    ( ( A XOR B ) XOR C ) = O1 (SUM)
For the AND, it was a little more complex, because that would revolve around the O2 as well, because when all three inputs are on both O1, the sum, and O2, the carry out, should dispay a 1, but the problem comes from the fact that O2 displays a 1 when more than 2 of the inputs are 1. So because of this, and the fact that C, the Carry in, could be 0 most of the time, I decided to have an AND gate that only outputs if A AND B are TRUE. However, O2 is not just 1 when only A and B are 1, it is on whenever either of A and B are 1, AND C is 1. So because of that I went back to the A XOR B gate that outputs to the XOR of C, and drew that output and put it into another AND gate that connects to C to test if only one out of A and B are true, with C being true simultaneously. To finalize the O2 output, I used an OR gate that gets input from the two different AND gates and outputs to O2.

    ( A AND B ) OR ( (A XOR B) AND C ) = O2 (CARRY OUT)

I initially thought I would need to wire the output of A AND B into the second layer of AND and XOR gates that draw one input from C and realized that through testing the truth table that it wasn't accurate, which made me realize that I  had made a mistake somewhere. After realizing my mistake and fixing it, I ran the same test cases from the truth table, and once that matched my created truth table I knew I could be confident that my circuit was a completed Full Adder.

After making my full adder i initally tried to wire 8 of them in sequence with the O2 (CARRY OUT) of each one going into the C (CARRY IN) of the next one, but when trying to wire my fifth full adder in the sequence in with the 5th B and A bits Logisim Evolution threw an Error called a "Nullpointer Exception", and after trying to see what caused it I just assumed it was a imposed wire limit per circuit and so instead of going from a Full adder directly to a working 8-bit adder I decided to make it a 4-bit adder, and wire two of those into a working 8-bit adder. I knew I didn't have to go into making it a 2-bit adder into a 4-bit adder and so on because I was able to wire 4 full adders together completely with Logisim only throwing the error when I tried to wire the fifth full adder. 
