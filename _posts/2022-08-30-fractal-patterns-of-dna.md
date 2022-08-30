---
title: Fractal patterns of DNA
layout: post
post-image: https://images.unsplash.com/photo-1643780668909-580822430155?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1032&q=80
description: 'Chaos Game Representation of DNA: visualizing the fractal structure
  of DNA sequences'
tags:
- dna
- fractals
- image
---

# Introduction 
In 1990, a reversible encoding for DNA inspired by the Chaos Game was introduced [1], which encodes a DNA sequence in a 2-dimensional point living in a square, where each vertex is associated with one character in the alphabet $\{A,C,G,T\}$. The main contribution was a new visualization of a DNA sequence based on the plot of all 2-dimensional points that arise from the step-by-step encoding, showing that for some sequences, fractal patterns can be seen. This encoding was named Chaos Game Representation of DNA (CGR). Years later, it was shown that the exact visualization can be generated using the k-mer frequencies of the sequence [2,3].

# Preliminaries
In order to understand this idea, we need a few concepts related to biological sequences and Chaos Game. 

Given the alphabet $\Sigma = \{A,C,G,T\}$, an $n$-long sequence will be denoted by $s=s[1]\dots s[n] \in \Sigma^n$. A subsequence of $s$ is any string $s[i:j]=s[i]\dots s[j]$, with $i\leq j$. For example, given the $6$-long sequence $s=ACGTCG$, then $s[2:4]=CGT$, and $s[3:3]=G=s[3]$. By convention, when $j<i$ we will denote $s[i:j]=\sigma$ as the empty string.

A $k$-mer is a subsequence of length $k<n$. Following our previous example, $s[2:4]=CGT$ correspond to a $3$-mer of the sequence $s$. All the $3$-mers of $s$ are $ACG,CGT,GTC,TCG$.

Notice that an $n$-long sequence has exactly $n-k+1$ $k$-mers. A very common task in bioinformatics is to find all $k$-mers in a sequence and their frequencies. This is not a trivial task when dealing with real data, the human genome, for example, is a 3-billion-long sequence. There exist specialized tools, like [KMC3]([https://academic.oup.com/bioinformatics/article/33/17/2759/3796399](https://academic.oup.com/bioinformatics/article/33/17/2759/3796399)), that can do the job efficiently for large sequences.

# Chaos Game: from Sierpinski triangle to CGR
The term Chaos Game refers to a method for creating a fractal from a polygon and random movements in the direction of the vertices. The resulting fractals are commonly known as Sierpinski polygons. For example, given a triangle, we start from a point in the center of the triangle, then we select randomly a vertex, and we move half of the distance between our current point to the vertex. The game continues starting from the last point, choosing again a vertex randomly and moving half of the distance in that direction. We repeat this process many times, and plotting all the points we will obtain the Sierpinski triangle as shown in the figure below.

![Sierpinski triangle: white areas correspond to areas where no points are plotted. Gray areas correspond to points that are selected from the Chaos Game procedure.](https://cdn.pixabay.com/photo/2015/03/29/01/06/mathematics-696806_960_720.png)

The Sierpinski triangle is a perfect mathematical fractal, like the Cantor Set. Every time we zoom in or zoom out, we will see the same patterns. There exist other kinds of fractals that arise from nature, but that is a story for another moment. Now let’s see how the same idea of Chaos Game can be used for DNA.

# Chaos Game representation of DNA (CGR)

The Chaos Game representation of DNA follows the same criteria as the Chaos Game but is restricted to a square, where each vertex is labeled by one character in the DNA alphabet $\{A,C,G,T\}$. One important detail is that now we do not select a vertex randomly, instead, given a sequence $s=s[1]\dots s[n]$, at each step $i$, we select the vertex labeled with the character $s[i]$ of the sequence, and we move half of the distance from our current position to that point (where the starting point is the center of the square). In the next video, I illustrate this procedure for the sequence $s=ACGGTC$

<iframe 
				width="640" 
				height="480" 
				src="https://www.youtube.com/embed/HU15ge0fkOY" 
				frameborder="0" 
				allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
				allowfullscreen
			>
</iframe>


Notice that from any encoding $(x,y)$ we can obtain the last character that was encoded by analyzing the signs of $x$ and $y$, if they are both positives, then the last character was an $A$, if $x<0$ and $y>0$, then the last character was a $C$, and so on. In synthesis, each quadrant will contain all the encodings of sequences that end in the label of its vertex. To make it clear, let’s see where are positioned all the sequences up to length $3$:

<iframe 
				width="640" 
				height="480" 
				src="https://www.youtube.com/embed/oYLT11Q9n5M" 
				frameborder="0" 
				allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
				allowfullscreen
			>
</iframe>

We can notice that a fractal pattern arises from the encoding, each quadrant is divided the same way as the original square. Moreover, sequences that end with the same subsequence, are encoded in a sub-square, for example, all sequences that end with $AA$ in the video, are placed in the right-top corner of the square. If we increase $k$, the square is subdivided into smaller squares, all of them sharing the same subsequence at the end, which we call the suffix of the sequence. 

Since our goal is to visualize the image that results from encoding all characters in the sequence and considering the fact that sequences that share the same suffix have an encoding that is close to each other in the square, up to a certain common $k$-long suffix, we are not able to distinguish (visually) between two of these encodings. For example, encodings of sequence $s=ACGTTT$ and $t=AAAAAACGTTT$ are $(0.796875, -0.890625)$ and $(0.81201171875,-0.87548828125)$, respectively. This allows us to generate the same figure from $k$-mers, we just need to count them and rescale the frequency to a grayscale value, and then generate the image. See the next video for an example.

<iframe 
				width="640" 
				height="480" 
				src="https://www.youtube.com/embed/hvjm8NLYM_4" 
				frameborder="0" 
				allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
				allowfullscreen
			>
</iframe>
# Bibliography
- [1] H Joel Jeffrey. Chaos game representation of gene structure. Nucleic acids research, 18(8):2163–2170, 1990.
- [2] Jonas S Almeida, Joao A Carrico, Antonio Maretzek, Peter A Noble, and Madilyn Fletcher. Analysis of genomic sequences by chaos game representation. Bioinformatics, 17(5):429–437, 2001.
- [3] Patrick J Deschavanne, Alain Giron, Joseph Vilain, Guillaume Fagot, and Bernard Fertil. Genomic signature: characterization and classification of species assessed by chaos game representation of sequences. Molecular biology and evolution, 16(10):1391–1399, 1999.