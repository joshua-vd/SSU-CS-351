# Project 4 - NVIDIA CUDA applications

## CUDA iota 

This program implements the std::iota function using CUDA.

## Timing Results 

Question: Are the results what you expected? Speculate as to why it looks like CUDA isn’t a great solution for this problem.

The results were mostly what I expected. The CUDA version was slower than the CPU version on this problem because the per-element work is very small. When the workload is small, CUDA is slower because the overhead of memory transfers and kernel launches outweighs the benefits of parallel execution. CUDA performs better when the workload is large. 

## Julia Set Generator 

This program generates a Julia/Mandelbrot set image using CUDA parallelism. Each GPU thread computes the color for a pixel in the image.

![Julia Set](julia.ppm) 
