# Basic Image Processing Library

We implemented an image processing library using the C programming language. The goal of this project is to implement useful image processing functionality so we used open source C code  to load and save the images. We used these save/load files to save us the trouble of writing it ourselves which increased development speed. This library can apply various filters, count and return connected black regions, create a feature vector based on a normalized ratio of black to white pixels, incorrectly thin and recognize digits.

## Convolutions

We implemented four different filters using convolutions that you can apply to an image of your choice. The four filters we provided are: outline, vertical sobel, blur, and high pass. The image is convoluted using the standard matrix multiplication method and then saved so you can view the result.

## Segmentation of Conntected Regions

Given an image with various greyscale valued regions our implementation identifies and counts each symbol. This is done by using a raster scan method which goes left to right, top to bottom by selecting a pixel and looking to its neighbors values. Everytime it encounters a new segment it gets identified and the pixel value changes to that segment value. In doing this we get connected regions with some neighboring segment values that are different, meaning they are connected but think they are different segments. To bypass this issue we keep track of which segment values are equivalent to each other. Returning the number of segments is done by looking at the equivalent regions and backtracking to its minimum equivalence and storing that value into a set. Taking the size of the set will return number of regions. To return the segment itself we store the minimum and maximum (x, y) values of each region and simply create a new image with the pixels seen within the minimum and maximum bounds of that selected region.

## Comparing Different Convolution Approaches

We apply two different colvolution approaches to the same image and compare the results. First we create a one by three horizontal filter and a three by one vertical filter where each value is ⅓. We then create a three by three filter filled with the same values as the other filters. First, we apply the horizontal filter, then vertical filter to the image. We then take the same original image and apply the three by three filter to it. Each convolution is done using the standard matrix multiplication method and both results are saved separately so you can compare them. The result of both operations is a blurred image. This shows that both approaches result in the same filtered image.

## Scaling

We implemented a scaling algorithm to scale down all of the symbols in any image. The symbols are scaled down by taking the average of every four pixel square and saving it as one pixel. This reduces the symbols in the image to a quarter of their previous size. Each symbol is is found by segmenting the image. Then each symbol is then scaled down with the top left corner of the symbol remaining is the same location. 

## Feature Vector

For the feature vector we decided to divide the image into sixteen quadrants instead of nine because we believe it produces a more accurate result. First we segment the input image to find all the different symbols and get each region. Then each symbol is split into 16 equal sections. The amount of black and white are found in each section. Then the number of black pixels are divided by the number of pixels in the section to get a normalized result between zero and one. The results of each section are written to a dataset as a feature vector to recognize characters.

## Character Recognition

Character recognition is done by creating a feature vector from a symbol and calculating the smallest difference between it and the other feature vectors in the dataset. The character to recognize is segmented to get an image of only the symbol and then it is converted to a feature vector. We compare the feature vector to all other feature vectors in the dataset. For each vector in the dataset, the difference between it and the vector to recognize is found between all of the features. All sixteen differences are added together. The vector with the least difference is most like the vector to recognize. 

# Authors

Adam Gumieniak
Brian Tiner
