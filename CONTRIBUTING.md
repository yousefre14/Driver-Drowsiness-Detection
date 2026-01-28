# Contributing to Driver Drowsiness Detection System

First off, thank you for considering contributing to this project! It's people like you that make this drowsiness detection system better for everyone.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Enhancements](#suggesting-enhancements)

## Code of Conduct

This project and everyone participating in it is governed by a simple principle: be respectful, be collaborative, and be constructive. We are all here to learn and improve the project together.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When creating a bug report, include:

- **Clear title and description**
- **Steps to reproduce** the issue
- **Expected behavior** vs actual behavior
- **System information** (OS, Python version, webcam model)
- **Screenshots or videos** if applicable
- **Error messages** or logs

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- **Clear use case** for the enhancement
- **Detailed description** of the proposed functionality
- **Why this enhancement would be useful** to most users
- **Possible implementation approach** (optional)

### Pull Requests

We actively welcome your pull requests! Here are some areas where contributions would be especially valuable:

- **Performance improvements** to the detection algorithm
- **Additional detection methods** (e.g., head pose, yawning detection)
- **Better alarm systems** (gradual alerts, different sound options)
- **GUI improvements** for easier configuration
- **Testing suite** with unit tests
- **Documentation improvements**
- **Multi-face tracking** support
- **Mobile platform support**
- **Different lighting condition optimization**

## Development Setup

1. Fork the repository to your own GitHub account
2. Clone your fork locally:
   ```bash
   git clone https://github.com/your-username/driver-drowsiness-detection.git
   cd driver-drowsiness-detection
   ```

3. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

5. Download the required model file:
   - Get `shape_predictor_68_face_landmarks.dat` from [dlib's models](http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2)

6. Create a new branch for your feature:
   ```bash
   git checkout -b feature/your-feature-name
   ```

## Pull Request Process

1. **Update documentation** if you've changed functionality
2. **Follow the coding standards** outlined below
3. **Test your changes** thoroughly with different scenarios:
   - Different lighting conditions
   - Different face angles
   - Multiple faces in frame (if applicable)
   - Various webcam resolutions

4. **Update the README.md** if needed with details of changes

5. **Commit with clear messages**:
   ```bash
   git commit -m "Add feature: brief description of what you did"
   ```

6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Open a Pull Request** with:
   - Clear title describing the change
   - Detailed description of what changed and why
   - References to any related issues
   - Screenshots/videos of new features in action

8. **Respond to feedback** - maintainers may request changes

## Coding Standards

### Python Style

- Follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guidelines
- Use meaningful variable and function names
- Add comments for complex logic
- Keep functions focused and modular

### Code Organization

```python
# Imports at the top, grouped by:
# 1. Standard library
# 2. Third-party packages
# 3. Local modules

# Constants in UPPER_CASE
EYE_AR_THRESH = 0.3

# Functions with docstrings
def eye_aspect_ratio(eye):
    """
    Calculate the eye aspect ratio (EAR) for drowsiness detection.
    
    Args:
        eye: Array of (x, y) coordinates for eye landmarks
        
    Returns:
        float: The computed eye aspect ratio
    """
    # Implementation
    pass
```

### Performance Considerations

- Optimize for real-time processing (target 30 FPS minimum)
- Avoid unnecessary computations in the main loop
- Use efficient NumPy operations where possible
- Profile code if making significant changes

### Testing

While we don't have a formal test suite yet, please manually test:

- Different lighting conditions (bright, dim, mixed)
- Various face angles and distances
- Edge cases (glasses, hats, etc.)
- Different webcam resolutions
- Performance on different hardware

## Feature Ideas

If you're looking for ideas on what to contribute, here are some suggestions:

### High Priority
- [ ] Add configuration file support (JSON/YAML)
- [ ] Implement logging system
- [ ] Create unit tests
- [ ] Add calibration mode for personalized thresholds
- [ ] Implement head pose estimation

### Medium Priority
- [ ] GUI for easier parameter adjustment
- [ ] Support for video file input (not just webcam)
- [ ] Multi-language support for alerts
- [ ] Statistics tracking (drowsiness events per session)
- [ ] Yawning detection

### Nice to Have
- [ ] Cloud logging for fleet management
- [ ] Mobile app version
- [ ] Integration with vehicle systems
- [ ] Multiple alert levels (warning, critical)
- [ ] Historical data visualization

## Questions?

Feel free to open an issue with the "question" label if you need clarification on anything!

## Attribution

Contributors will be acknowledged in the project README. Thank you for making this project better!
