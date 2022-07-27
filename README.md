# JoinSketch

## Introduction
Inner-product estimation is the base of many important tasks in a variety of big data scenarios, including measuring similarity of streams in data stream processing, estimating join size in database, and analysing cosine similarity in various applications.
Sketch, as a class of probability algorithms, is promising in inner-product estimation.
However, existing sketch solutions suffer from low accuracy due to their neglect of the high skewness of real data.
We design a new sketch algorithm for accurate and unbiased inner-product estimation, namely JoinSketch.
To improve accuracy, JoinSketch consists of multiple components, and records items with different frequency in different components.
We theoretically prove that JoinSketch is unbiased, and has lower variance compared with the well-known AGMS and Fast-AGMS sketch.
The experimental results show that JoinSketch improves the accuracy by $10$ times in average while maintaining a comparable speed.

## Requirements

- CMake
- g++
- C++11
- Boost

## File Structure

*  `datasets/`: The sample datasets extracted from the real-world datasets used in our experiments.
*  `src/`: The source codes of JoinSketch and the algorithms we compared with.

## Datasets

- ` CAIDA.dat` We provide a fragment of the CAIDA dataset, and when reading a single CAIDA dataset file we will treat the first and second halves as two data streams.

- `zipf` We generate a series of synthetic datasets that follow the Zipf distribution. The skewness of the datasets range from 0.0 to 1.0. Each dataset contains approximately 1.0M flows, 32.0M items. The length of each item ID is 4 bytes.

For more details, please refer to our paper. 

## Run tests

You can use the following commands to build and run our tests. 

```bash
$ cd src
$ make
$ ./main [-f filename] [-l keylen] [-m memory] [-v version]
```

1. `[-f filename]`: The path of the dataset you want to run. 
2. `[-l keylen]`: An integer, representing the length of each entry in the dataset.
3. `[-m memory]`: An integer, represeting the memory size (in bytes) used by the JoinSketch. 
4. `[-v version]`: An integer, representing the algorithm you want to run. You can refer to `include/Choose_Ske.h`

You can modify the `Heavy_Thes` in `main.cpp` to adapt to different datasets.

### Output Format

Our program will print the statistics about the input dataset and the parameters of the candidate algorithms at the command-line interface. Then our program will generate a file `result.csv` containing information such as mean error, variance, max min and throughput.
