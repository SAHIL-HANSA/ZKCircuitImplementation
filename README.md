# Polygon Proof Advance: ZKEVM Circuit

**Custom Circuit Template**
This circuit template is designed to check if signal c is the result of the multiplication of signals a and b. The circuit is implemented using the circom language version 2.0.0.

The circuit consists of three main components: AND, NOT, and OR. The AND component computes the logical AND operation between two input signals (a and b). The NOT component computes the logical NOT operation on its input signal (b). The OR component computes the logical OR operation between its two input signals (x and y).

The circuit template MyCustomCircuit uses these components to perform the multiplication check. The inputs a and b represent the numbers to be multiplied. The circuit computes x, which is the result of the logical AND between a and b. It also computes y, which is the logical NOT of b. Finally, the circuit outputs q, which is the result of the logical OR between x and y.

MyCustomCircuit:

    pragma circom 2.0.0;
    
    /*This circuit template checks that c is the multiplication of a and b.*/  
    
    template MyCustomCircuit () {  
       // signal inputs
       signal input a;
       signal input b;
    
       // signal from gates
       signal x;
       signal y;
    
       // final signal output
       signal output q;
    
       // component gates used to create custom circuits
       component andGate = AND();
       component notGate = NOT();
       component orGate = OR();
    
       // circuit logic 
       andGate.a <== a;
       andGate.b <== b;
       x <== andGate.out;
    
       notGate.in <== b;
       y <== notGate.out;
    
       orGate.a <== x;
       orGate.b <== y;
       q <== orGate.out;
    }
    
    template AND() {
        signal input a;
        signal input b;
        signal output out;
    
        out <== a*b;
    }
    
    template NOT() {
        signal input in;
        signal output out;
    
        out <== 1 + in - 2*in;
    }
    
    template OR() {
        signal input a;
        signal input b;
        signal output out;
    
        out <== a + b - a*b;
    }

AND
The AND component takes two input signals (a and b) and outputs their logical AND:

    template AND() {
        signal input a;
        signal input b;
        signal output out;
    
        out <== a * b;
    }

NOT
The NOT component takes one input signal (in) and outputs its logical NOT:

    template NOT() {
        signal input in;
        signal output out;
    
        out <== 1 + in - 2 * in;
    }


OR
The OR component takes two input signals (a and b) and outputs their logical OR:

    template OR() {
        signal input a;
        signal input b;
        signal output out;
    
        out <== a + b - a * b;
    }

By evaluating the output signal q, you can determine if q is the multiplication of a and b. If q is true, then c is the result of the multiplication; otherwise, it is not.

## License
This project is licensed under MIT.
