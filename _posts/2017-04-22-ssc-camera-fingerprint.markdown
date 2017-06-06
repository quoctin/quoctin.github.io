---
layout: post
title:  "Camera Fingerprint Clustering"
date:   2017-04-20 16:00 -0200
description: This project aims at developing unsupervised techniques to cluster images by their acquisition device
permalink: /ssc-camera-fingerprint/
---

## Summarization

<p align="justify">
  Each digital image contains a unique intrinsic trace left by the camera through the image acquisition process, the so-called <em>camera fingerprint</em>. Such camera fingerprint uniquely identifies the acquisition camera and can be exploited for multiple forensic purposes. Up-to-date technologies enable camera fingerprint estimation if an analyst has the suspected device in hand, or a set of original images proved to be taken by that camera. In practical applications, it is difficult to fulfill those requirements since often only a set of unsourced images is available to forensic investigators. In order to deal with those circumstances, grouping images with respect to their acquisition cameras is a preliminary step before performing other forensic steps, i.e., estimating the number of cameras, estimating reliable camera fingerprints, linking a suspected image to one cluster with a certain level of confidence.
</p>
<p align="justify">
  In the literature, unsupervised learning techniques have been proposed in order to group images taken by the same camera together. Most of those techniques use normalized correlation of two fingerprints as similarity measurement. In this work, we aim to solve the problem by finding sparse representations of Sensor Pattern Noises (SPNs) which characterize underlying data segmentation.
</p>
<p align="justify">
  Although camera fingerprints are represented in high dimensional space, their intrinsic dimension is often much smaller. SPNs of the same camera can be interpreted as lying in a subspace whose dimension is much smaller than the dimension of the ambient space.
</p>

<img src="/assets/img/SSC/sparse-model.pdf" width="500" />
<p align="middle">Figure 1. Sparse representation model of camera fingerprints.</p>

<p>
  We show that solving \(\ell_1\)--regularized least squares can recover sparse representations of data.
</p>

## References
  1. **Quoc-Tin Phan**, Giulia Boato, and Francesco G. B. De Natale, *Image Clustering by Source Camera via Sparse Representation,* [[PDF](/files/MFSec2017.pdf)]
