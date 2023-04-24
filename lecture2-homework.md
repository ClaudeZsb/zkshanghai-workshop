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
```
pragma circom 2.1.4;

template IsZero() {
    signal input in;
    signal output out;

    signal inv;
    inv <-- (in == 0) ? 1 : 1/in;
    out <== 1 - in * inv;
    0 === in * out;
}

component main = IsZero();

/* INPUT = {
    "in": "0"
} */
```

## 第3题 IsEqual
```
pragma circom 2.1.4;

template IsEqual() {
    signal input in[2];
    signal output out;

    component isZero = IsZero();
    isZero.in <== in[0] - in[1];
    out <== isZero.out;
}

component main = IsEqual();

/* INPUT = {
    "in": ["0", "1"]
} */
```

## 第4题 Selector
```
pragma circom 2.1.4;

template Selector(nChoices) {
    signal input in[nChoices];
    signal input index;
    signal output out;

    component isEqual[nChoices];
    var sum = 0;
    signal internalValues[nChoices];
    for(var i = 0; i < nChoices; i++) {
        isEqual[i] = IsEqual();
        isEqual[i].in[0] <== i;
        isEqual[i].in[1] <== index;
        internalValues[i] <== isEqual[i].out * in[i];
        sum += internalValues[i];
    }

    out <== sum;
}

component main = Selector(6);

/* INPUT = {
    "in": ["0", "1", "2", "3", "4", "5"],
    "index": "6"
} */
```

## 第5题 IsNegative

## 第6题 LessThan

## 第7题 IntergerDivide

## 第8题 BubbleSort

