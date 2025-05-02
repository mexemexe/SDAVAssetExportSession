# SDAVAssetExportSession: Flexible iOS Media Transcoding Library

## Project Overview

SDAVAssetExportSession is a powerful iOS library that provides a flexible alternative to Apple's `AVAssetExportSession` for media asset transcoding. While the standard `AVAssetExportSession` limits developers to predefined presets, this library offers full customization of audio and video export settings.

### Key Features

- **Customizable Media Export**: Complete control over audio and video encoding settings
- **Asynchronous Export**: Seamless background processing of media assets
- **Flexible Configuration**: Supports custom video composition and audio mixing
- **Network Optimization**: Option to optimize exported media for network use
- **Detailed Progress Tracking**: Provides real-time export progress monitoring

### Problem Solved

Media transcoding on iOS can be challenging due to the rigid preset limitations of `AVAssetExportSession`. This library eliminates those constraints, allowing developers to precisely define output media characteristics such as resolution, bitrate, codec, and more. Whether you need to create thumbnails, compress videos, or prepare media for specific platforms, SDAVAssetExportSession provides the flexibility required for advanced media processing tasks.

## Getting Started, Installation, and Setup

### Prerequisites
- iOS 6.0 or later
- Objective-C project
- Compatible with ARC (Automatic Reference Counting)

### Installation

#### CocoaPods
Add the following to your `Podfile`:
```ruby
pod 'SDAVAssetExportSession'
```

#### Manual Installation
1. Clone the repository
2. Add `SDAVAssetExportSession.h` and `SDAVAssetExportSession.m` to your project
3. Import the header in your code: `#import "SDAVAssetExportSession.h"`

### Quick Start

```objective-c
// Create an export session with your input asset
SDAVAssetExportSession *encoder = [SDAVAssetExportSession.alloc initWithAsset:anAsset];

// Configure output settings
encoder.outputFileType = AVFileTypeMPEG4;
encoder.outputURL = outputFileURL;

// Customize video settings
encoder.videoSettings = @{
    AVVideoCodecKey: AVVideoCodecH264,
    AVVideoWidthKey: @1920,
    AVVideoHeightKey: @1080,
    AVVideoCompressionPropertiesKey: @{
        AVVideoAverageBitRateKey: @6000000,
        AVVideoProfileLevelKey: AVVideoProfileLevelH264High40,
    },
};

// Customize audio settings
encoder.audioSettings = @{
    AVFormatIDKey: @(kAudioFormatMPEG4AAC),
    AVNumberOfChannelsKey: @2,
    AVSampleRateKey: @44100,
    AVEncoderBitRateKey: @128000,
};

// Export the asset
[encoder exportAsynchronouslyWithCompletionHandler:^{
    if (encoder.status == AVAssetExportSessionStatusCompleted) {
        NSLog(@"Video export succeeded");
    } else if (encoder.status == AVAssetExportSessionStatusCancelled) {
        NSLog(@"Video export cancelled");
    } else {
        NSLog(@"Video export failed with error: %@ (%d)", 
              encoder.error.localizedDescription, encoder.error.code);
    }
}];
```

### Customization
`SDAVAssetExportSession` provides granular control over audio and video export settings. You can:
- Set custom video codec
- Define precise video dimensions
- Configure bitrate and profile levels
- Customize audio format, channels, and encoding

### Compatibility
- Supports iOS 6.0+
- Works with any asset compatible with `AVAssetExportSession`
- Provides more flexibility than standard `AVAssetExportSession`

## Project Structure

The project is a lightweight Objective-C library with a minimal file structure:

#### Source Files
- `SDAVAssetExportSession.h`: Header file defining the main interface for the `SDAVAssetExportSession` class
- `SDAVAssetExportSession.m`: Implementation file containing the core logic for the export session

#### Metadata Files
- `SDAVAssetExportSession.podspec`: CocoaPods specification file for dependency management
- `LICENSE`: MIT license file detailing the terms of use
- `.gitignore`: Git ignore configuration to exclude unnecessary files from version control

#### Key Components
The project revolves around a single primary class `SDAVAssetExportSession`, which provides a flexible alternative to Apple's `AVAssetExportSession`. It allows custom audio and video encoding settings for media asset export, implemented as a drop-in replacement with enhanced customization capabilities.

## Technologies Used

### Platforms
- iOS (minimum version 6.0)

### Programming Languages
- Objective-C

### Frameworks
- AVFoundation
  - `AVAssetReader`
  - `AVAssetWriter`
  - `AVAssetReaderVideoCompositionOutput`
  - `AVAssetReaderAudioMixOutput`
  - `AVAssetWriterInput`

### Key Technologies
- Video Encoding
- Audio Encoding
- Media Asset Processing

### Supported Video Codecs
- H.264

### Supported Audio Formats
- AAC

### Development Tools
- CocoaPods (dependency management)
- Xcode (iOS development environment)

### Licensing
- MIT License

## Additional Notes

### Performance Considerations

When using `SDAVAssetExportSession`, keep in mind the computational intensity of video transcoding. The custom video and audio settings provide flexibility but may impact export performance depending on the complexity of the conversion.

### Delegate Support

The library provides a delegate protocol `SDAVAssetExportSessionDelegate` that allows for advanced frame rendering customization. Implement this protocol if you need fine-grained control over individual frame processing during export.

### Error Handling

Always check the `status` and `error` properties after export completion. The export can fail due to various reasons such as:
- Incompatible video or audio settings
- Insufficient system resources
- Invalid input asset
- Permissions or file system issues

### Supported Platforms

This library is designed for iOS and requires AVFoundation. It is compatible with iOS versions supporting the underlying AVFoundation classes.

### Memory Management

Be cautious with large video files, as the export process can be memory-intensive. Consider implementing progress tracking and potentially breaking large exports into smaller segments if memory is a concern.

### Codec and Format Compatibility

While the library offers extensive customization, not all video codecs and settings are universally supported. Test thoroughly with your specific use cases and target devices.

## Contributing

We welcome contributions to SDAVAssetExportSession! By contributing, you can help improve this library for the entire community.

### How to Contribute

1. Fork the repository
2. Create a new branch for your feature or bugfix
3. Make your changes, ensuring you follow these guidelines:
   - Write clean, readable, and well-commented Objective-C code
   - Maintain the existing code style and conventions
   - Add or update tests to cover your changes
   - Ensure all existing tests pass

### Contribution Process

- Open an issue to discuss significant changes before submitting a pull request
- Submit pull requests to the `master` branch
- Provide a clear and descriptive commit message
- Include a description of the problem you're solving or feature you're adding

### Code of Conduct

- Be respectful and considerate of other contributors
- Provide constructive feedback
- Focus on the quality of the code and the project's goals

### Reporting Issues

If you find a bug or have a suggestion:
- Check existing issues to avoid duplicates
- Use the GitHub issue tracker
- Provide detailed information, including:
  - Steps to reproduce the issue
  - Expected behavior
  - Actual behavior
  - Your environment (Xcode version, iOS version, etc.)

### Development Setup

- Xcode is required for development
- Use the provided `.xcworkspace` or `.xcodeproj` for development
- Recommended: Use the latest stable version of Xcode

### Pull Request Guidelines

- Keep pull requests focused and concise
- Address only one issue or feature per pull request
- Include unit tests for new functionality
- Ensure all tests pass before submitting

Thank you for contributing to SDAVAssetExportSession!

## License

This project is licensed under the MIT License. 

#### License Details
- Full license text is available in the [LICENSE](LICENSE) file
- Copyright (c) 2013 Olivier Poitrey

#### Key Permissions
- Commercial use
- Modification
- Distribution
- Private use

#### Conditions
- License and copyright notice must be included
- Provided without warranty

For complete details, please refer to the full [LICENSE](LICENSE) file.