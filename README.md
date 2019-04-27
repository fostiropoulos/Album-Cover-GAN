# Go Deep or Go Home


Using GANs to generate Art
![](https://skymind.ai/images/wiki/GANs.png)
Experimenting with different GAN architectures to generate art that correlates the song genre to the album cover


# Music Album Cover Generation from Music Track with Conditional Generative Adversarial Network
Anna Nadtochiy, Iordanis Fostiropoulos, Syamil Mohd Razak, Takato Goto  
University of Southern California, Los Angeles, CA, USA  
{nadtochi, fostirop, mohdraza, tgoto}@usc.edu  
## Introduction
### Goals
- Learn the relationship between the songs and the album covers as the visual  
- Generate album covers conditioned to a music track  

<img src="https://user-images.githubusercontent.com/42685217/56783671-b96f8580-67a1-11e9-9ded-6a0b57aa3a73.png" width="1024">
Samples of cover albums from two distinct groups genre show similarities of features and styles within each genre. Death metal music and jazz music are undeniably distinct.  

### Problem Formulation
<img src="https://user-images.githubusercontent.com/42685217/56784100-d60cbd00-67a3-11e9-86f5-8c2dda3901fb.png" width="1024">


## Framework
### Encoding function &Phi;  
- Extract features from music track to be used as conditional data
### Conditional GAN
- Condition on music track features  
- Generate complex and diverse album covers  
<img src="https://user-images.githubusercontent.com/42685217/56784170-179d6800-67a4-11e9-9048-efe36271e073.png" width="1024">

## Encoding functions
### Various dimensionality reduction techniques are used to identify groups/genres in music tracks
1. Reduce the dimension of music spectral and rhythm features using PCA  
2. Using RNN as a feature extraction method to account for temporal variation in music tracks  
3. Reduce the dimension of music spectral and rhythm features using auto-encoder  
4. Converting music tracks to spectrogram and using CNN as a feature extraction (CNN was trained to classify the music genre)   
<img src="https://user-images.githubusercontent.com/42685217/56784466-7b746080-67a5-11e9-9e90-c54d5469ef15.png" width="256">　<img src="https://user-images.githubusercontent.com/42685217/56784471-7ca58d80-67a5-11e9-9e38-c978bd28203c.png" width="256">

Samples of album covers from two distinct groups of genre show similarities of features and styles within each genre (different colors). Death metal (dark blue) and jazz (red) music are undeniably distinct, but album covers are not.  

![06](https://user-images.githubusercontent.com/42685217/56784691-bb881300-67a6-11e9-988a-f71bc4bf0efc.png)
![07](https://user-images.githubusercontent.com/42685217/56784693-bd51d680-67a6-11e9-92cc-0e90c2e42531.png)
Raw mp3 files encoded in lower dimension as a compact representation of the music track. Different genres are shown in different colors.  
![08](https://user-images.githubusercontent.com/42685217/56784762-09048000-67a7-11e9-9972-b9be9cbbe5eb.png)
![09](https://user-images.githubusercontent.com/42685217/56784910-cabb9080-67a7-11e9-8c10-6d85f53af355.png)
Features extracted by LibROSA are reduced in dimension using an auto-encoder. Features can be split into 4 clusters (different color).  
![10](https://user-images.githubusercontent.com/42685217/56784831-64367280-67a7-11e9-8c0b-76e29602767e.png)
![11](https://user-images.githubusercontent.com/42685217/56784833-66003600-67a7-11e9-97b1-72521930f838.png)
Music track, represented as spectrogram, classified into 8 distinct genres using CNN.  
## GAN Architectures
### Various GANs have been tested to see if they have the capacity to represent and generate complex unstructured images
[![Style Gan on Album Covers](https://img.youtube.com/vi/8a0zIEanp6A&feature=youtu.be/.jpg)](https://www.youtube.com/watch?v=8a0zIEanp6A&feature=youtu.be)  
WGAN-GP (64x64)  
![12](https://user-images.githubusercontent.com/42685217/56785149-b1ffaa80-67a8-11e9-9315-8d212ab60c37.png)
DCGAN (64x64) 
![13](https://user-images.githubusercontent.com/42685217/56785151-b330d780-67a8-11e9-8da6-a052b5adb428.png)
WGAN-G adn DCGAN produce abstract shapes  
Style GAN (256x256) 
![14](https://user-images.githubusercontent.com/42685217/56785159-b62bc800-67a8-11e9-9cfd-8c40f7db8623.png)
The most realistic looking compared to all other architectures, produces file details (faces, text)  

Cover albums stored by proximity according to t-SNE.
![15](https://user-images.githubusercontent.com/42685217/56785163-b9bf4f00-67a8-11e9-9a21-4d72ea13018b.png)
Album covers are arranged according to RGB colors and weakly by structures and not by the genre they belong to.  

### Conditional GAN
We modified WGAN and Style GAN to take condition (i.e. music features) as input.
![16](https://user-images.githubusercontent.com/42685217/56785338-98ab2e00-67a9-11e9-9d2f-84344b7a8508.png)
Architecture of a conditional GAN that we adopt to introduce a conditioning vector of music track in reduced dimension
![18](https://user-images.githubusercontent.com/42685217/56844674-ecc91780-6868-11e9-86c5-71b356a2cb6b.png)
To use the pre-trained unconditioned StyleGAN: find the correspondence between the music track latent space the unit variance Gaussian noise vector.  
StyleGAN latent space interpolation


## Discussion
- Relationship between music tracks and album covers may not exist, very complex or is not made obvious through the analysis we have performed
- As a result, the images generated conditioned on either low dimensional representation of music track or arbitrary groups assigned to album covers do not belong to the same distribution as the original groups
- Due to the (perhaps) non-existent relationship between music track and album covers, it’s not as straight-forward to validate if the conditioning has actually worked

## Conclusion
- Style GAN can effectively represent complex unstructured images of album covers
- Album covers can be clustered according to RGB color or high-level drawing style, but not the album genre
- Music tracks can be classified by genres and represented in lower dimension effectively


### Dataset
The dataset used in this project has been collected through Spotify API and includes 50,000 high resolution (640x640) cover album and corresponding music 30 sec. long tracs in mp3 format. Dataset also includes extracted attributes such as danceability, energy, loudness, speechiness, etc. Available at https://drive.google.com/file/d/1nmurIZw8cyrfziCH5d6WOrxRBriT0Oet/view

### Reference
Scott E. Reed, Zeynep Akata, Xinchen Yan, Lajanugen Logeswaran, Bernt Schiele, and Honglak Lee.Generative adversarial text to image synthesis.CoRR, abs/1605.05396, 2016.  
WGAN-GP  https://github.com/shaohua0116/WGAN-GP-TensorFlow  
StyleGAN  https://github.com/NVlabs/stylegan  
DCGAN  https://github.com/carpedm20/DCGAN-tensorflow  
Genre classification  https://github.com/Jonalkn/CS230_FINAL_PROJECT
