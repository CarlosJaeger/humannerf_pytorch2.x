# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.1.0] - 2025-10-24
### Changed
- **core/utils/network_util.py**: Updated the `initmod` function.  
  - Replaced direct `.data` tensor modification with `torch.no_grad()` context.  
  - Added safety check to ensure `m.bias` is not `None` before zeroing.  
  - This improves compatibility with modern PyTorch (>= 2.x) and avoids deprecated `.data` usage.

- **core/utils/network_util.py**: Updated the `xavier_uniform_` function.  
  - Replaced usage of `.data` with `torch.no_grad()` context for weight initialization.  
  - Ensures safer and future-proof initialization in compliance with modern PyTorch practices.

- **core/utils/network_util.py**: Refactored the `RodriguezModule` normalization routine.  
  - Replaced manual computation of vector norm (`sqrt(1e-5 + sum(rvec**2))`) with `torch.norm(...).clamp_min(1e-5)`.  
  - This modification ensures numerical stability by preventing division by zero and mitigates the risk of NaN values. 

  - **core/utils/network_util.py**: Revised the `MotionBasisComputer` implementation.  
  - Replaced deprecated `torch.inverse` with `torch.linalg.inv`.  
  - This update aligns the codebase with the recommended `torch.linalg` API, ensuring forward compatibility with future PyTorch releases.
