# 第2课 课后作业

## 第1题 Num2Bits

```
pragma circom 2.1.4;

template Num2Bits (nbits) {
    signal input in;
    signal output b[nbits];
    assert(in <= 2<<nbits);
    
    var sum = 0;
    var cur = 1;
    for(var i = 0; i < nbits; i++) {
        b[i] <-- (in >> i) & 1;
        0 === b[i] * (1 - b[i]);
        sum += cur * b[i];
        cur = cur * 2;
    }

    sum === in;
}

component main = Num2Bits(4);

/* INPUT = {
    "in": "9"
} */
```

## 第2题 IsZero

## 第3题 IsEqual

## 第4题 Selector

## 第5题 IsNegative

## 第6题 LessThan

## 第7题 IntergerDivide

## 第8题 BubbleSort

