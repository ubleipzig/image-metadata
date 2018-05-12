## Image 
A collection of image processing utilities

### Image Metadata
A utility that generates JSON objects that contain image metadata.

[![Build Status](https://travis-ci.org/ubleipzig/image.png?branch=master)](https://travis-ci.org/ubleipzig/image)
[![codecov](https://codecov.io/gh/ubleipzig/image/branch/master/graph/badge.svg)](https://codecov.io/gh/ubleipzig/image)
[![Javadoc](https://javadoc-badge.appspot.com/de.ubleipzig/image.metadata.svg?label=javadoc)](https://ubleipzig.github.io/image/apidocs/)
[![Maven Central](https://img.shields.io/maven-central/v/de.ubleipzig/image.metadata.svg)](https://mvnrepository.com/artifact/de.ubleipzig/image.metadata/0.1.0)


#### Install
`./gradlew clean distTar`

* extract `image.metadata-0.2.0-SNAPSHOT.tar`

## Sequenced Image Filename Specification
This tool assumes that all images will have integer filenames in accordance with their sequence in the image collection.

#### Run as Utility from CLI

```bash
./image.metadata -i {$image_source_directory} -o {$dimension_manifest_output_file_path} -z {$metadata_manifest_output_path} (optional)
```

#### Use in Java:

```groovy
 compile group: 'de.ubleipzig', name: 'image.metadata', version: '0.1.0'
```


* Generate an image dimension manifest with :

```java
/**
* @param String imageSourceDir
*/
```

```java
    ImageMetadataServiceConfig config = new ImageMetadataServiceConfig();
    config.setImageSourceDir(imageSourceDir);
    final ImageMetadataService generator = new ImageMetadataServiceImpl(config);
    final ImageDimensionManifest dimManifest = generator.build();
```

The dimension manifest when serialized looks like this:
```json
{
  "collection" : "/some-image-collection",
  "images" : [
    {
      "filename" : "00000001.jpg",
      "digest" : "jeUrOCoqaYw/89LmIo3gQlxhipE=",
      "height" : 2130,
      "width" : 1705
    },
    {
      "filename" : "00000002.jpg",
      "digest" : "5t/uKe+X1vTe0fR2YAGYj4OzgiI=",
      "height" : 2130,
      "width" : 1705
    },
    {
      "filename" : "00000003.jpg",
      "digest" : "8caG/XPRwwAZSU3Pldcsl7ZEtoA=",
      "height" : 2130,
      "width" : 1705
    }
  ]
}
``` 

The `ImageDimensionManifest` is a `List<ImageDimensions>` where each `ImageDimension` has setter and getters available 
for subsequent processing.

Also available is the complete list of `ImageMetadataTag`.  This `ImageMetadataManifest` can be built like this:

```java
    ImageMetadataServiceConfig config = new ImageMetadataServiceConfig();
    config.setImageSourceDir(imageSourceDir);
    final ImageMetadataService generator = new ImageMetadataServiceImpl(config);
    final ImageDimensionManifest dimManifest = generator.buildImageMetadataManifest();
```

An typical JPEG image produces this:

```json
    {
      "filename" : "00000001.jpg",
      "digest" : "jeUrOCoqaYw/89LmIo3gQlxhipE=",
      "directories" : [
        {
          "directory" : "JPEG",
          "tags" : [
            {
              "tagName" : "Compression Type",
              "tagDescription" : "Baseline"
            },
            {
              "tagName" : "Data Precision",
              "tagDescription" : "8 bits"
            },
            {
              "tagName" : "Image Height",
              "tagDescription" : "2130 pixels"
            },
            {
              "tagName" : "Image Width",
              "tagDescription" : "1705 pixels"
            },
            {
              "tagName" : "Number of Components",
              "tagDescription" : "3"
            },
            {
              "tagName" : "Component 1",
              "tagDescription" : "Y component: Quantization table 0, Sampling factors 2 horiz/2 vert"
            },
            {
              "tagName" : "Component 2",
              "tagDescription" : "Cb component: Quantization table 1, Sampling factors 1 horiz/1 vert"
            },
            {
              "tagName" : "Component 3",
              "tagDescription" : "Cr component: Quantization table 1, Sampling factors 1 horiz/1 vert"
            }
          ]
        },
        {
          "directory" : "JpegComment",
          "tags" : [
            {
              "tagName" : "JPEG Comment",
              "tagDescription" : "Generated by IIPImage"
            }
          ]
        },
        {
          "directory" : "JFIF",
          "tags" : [
            {
              "tagName" : "Version",
              "tagDescription" : "1.1"
            },
            {
              "tagName" : "Resolution Units",
              "tagDescription" : "none"
            },
            {
              "tagName" : "X Resolution",
              "tagDescription" : "1 dot"
            },
            {
              "tagName" : "Y Resolution",
              "tagDescription" : "1 dot"
            },
            {
              "tagName" : "Thumbnail Width Pixels",
              "tagDescription" : "0"
            },
            {
              "tagName" : "Thumbnail Height Pixels",
              "tagDescription" : "0"
            }
          ]
        },
        {
          "directory" : "Huffman",
          "tags" : [
            {
              "tagName" : "Number of Tables",
              "tagDescription" : "4 Huffman tables"
            }
          ]
        },
        {
          "directory" : "File Type",
          "tags" : [
            {
              "tagName" : "Detected File Type Name",
              "tagDescription" : "JPEG"
            },
            {
              "tagName" : "Detected File Type Long Name",
              "tagDescription" : "Joint Photographic Experts Group"
            },
            {
              "tagName" : "Detected MIME Type",
              "tagDescription" : "image/jpeg"
            },
            {
              "tagName" : "Expected File Name Extension",
              "tagDescription" : "jpg"
            }
          ]
        }
      ]
    }
```    
    
## Credits
This library depends on the [com.drewnoakes:metadata-extractor](https://github.com/drewnoakes/metadata-extractor)    
