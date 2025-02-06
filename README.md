# 🧮 Basis-Vector-Encoding
<!-- # 🚧🏗️ In Progress... -->
<br>

## **🔍 Portfolio Project Showcase**  
*This is a conceptual demonstration, not production-ready code.*  


### **✨ Key Concepts Demonstrated**  
| **Concept**               | **Implementation Example**                      |  
|---------------------------|-------------------------------------------------|  
| **Basis Vectors**          | Custom basis matrices define new coordinate systems for message projection |  
| **Coordinate System Conversion** | Messages transformed between standard basis ↔ arbitrary basis spaces |  
| **Linear Transformation** | Matrix operations applied to vectors during encoding/decoding |  
| **Basis Change**           | Messages re-encoded using transformation matrices between systems |  
| **Inverse Transformations**| Message recovery through matrix inversion operations |  

<br>

**Key Notes:**  
⚠️ Prioritizes mathematical clarity over practicality  
⚠️ Intentional unoptimized implementation **to showcase step-by-step logic and enhance code clarity**  
⚠️ Serves as skills exhibit for technical interviews  


<br>

## **📖 Description**

This project encodes and decodes messages using basis vectors. 
In simple terms, think of it as a way of transforming a message into a different 'language'—where each set of basis vectors represents a specific perspective or coordinate system. To decode the message, you need to have the appropriate 'translation'—the corresponding basis vectors from that same 'language.' 

While this project doesn't have much practical use, it serves as a portfolio piece to demonstrate my understanding of basis change, linear transformations, and mathematical concepts.


## **📂 Project Structure**  
| File                     | Purpose                                  |  
|--------------------------|------------------------------------------|  
| `main.py`                | Core encoding/decoding logic            |  
| `tools.py`               | Vector class & transformation utilities |  
| `symbol_mapping.json`    | Maps 95+ symbols to ℝⁿ coordinates      |  

## 🛠️ Usage

Disclaimer: This project is intentionally non-practical and serves as a learning tool.

2. Explanation of main.py
3. Explanation of symbol_mapping.json




## Workflow

So, how the code works? Here is a step by step explanation.

1. The goal of a file is to encode a string message in specific coordinate system (described by specific basis matrix). Then we decode the same encoded message, using basis representation of that coordinate system in another coordinate system (Jenifer's basis vectors represented using Mike's basis vectors)

2. To do all of the described operations, first we need to map each symbol to a vector in space. For this, we read `symbol_mapping.json` which is file that mapps each symbol/token to an integer.
It also contains `UNK` (Unkown Token) and `PAD` (Padding Token). Mapping symbols in vectors in such way implicitly makes them in std basis.
```json
{
    "UNK": -1,
    "PAD": 70,
    "a": 1,
    "b": 2,
    "c": 3,
    "d": 4,
    "e": 5,
    ...
    "\\": 65,
    "|": 66,
    "`": 67,
    "~": 68,
    " ": 69

}
```

3. We use `encrypt()` functions  to map each symbol. Then we pad it based on the dimensions of the basis matrix provided (2, 3, ...). Then we vectorize them using `Vector` class and transform using new basis matrix.

4. In `decrypt()` function, we pass the encrypted message along with the same basis represenation of the basis we used to encode the message. Note: We must pass to `decrypt()` function the same basis change representaion matrix as to `encrypt()` function. That transformation matrix says "Jenifer's basis vectors in Mike's perspective/ described by vectors in the Mike's coordinate system".

Additional Notes:

- In this implementation, each symbol in the string corresponds to a single vector.
- Vector() class is a simple overlay  of np.ndarray with just a simple shape manipulation and clarity in names