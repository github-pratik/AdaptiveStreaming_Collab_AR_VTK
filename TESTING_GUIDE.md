# 🧪 CIA_Web Testing Guide

**Comprehensive Testing Guide for Collaborative Immersive Analysis on the Web**

---

## 🚀 Quick Start

### Prerequisites
- Node.js (v16+)
- Modern web browser (Chrome/Edge recommended for WebXR)
- VR headset (optional, for VR testing)

### Running the Application
1. **Start WebSocket Server:**
   ```bash
   node server.js
   ```
   - Server runs on `ws://localhost:9001`
   - Handles real-time collaboration

2. **Start Development Server:**
   ```bash
   npm start
   ```
   - Application runs on `http://localhost:8080`
   - Auto-opens in browser

---

## 📋 Core Functionality Tests

### 1. **File Loading & Visualization**

#### Test 1.1: Basic VTP File Loading
**Objective:** Verify VTP file loading and 3D visualization

**Steps:**
1. Open `http://localhost:8080`
2. Click "Choose File" or drag a `.vtp` file from `vtp_files/` folder
3. Select one of the sample files:
   - `Bones.vtp` - Skeletal structure
   - `Lungs.vtp` - Lung anatomy
   - `Skull.vtp` - Skull model
   - `Ventricles.vtp` - Brain ventricles

**Expected Results:**
- ✅ File loads successfully
- ✅ 3D model renders in viewport
- ✅ Orientation marker appears (bottom-right corner)
- ✅ Log shows: "File loaded successfully!"
- ✅ Dataset information displayed (points, bounds, polygons)

**Troubleshooting:**
- If file doesn't load: Check browser console for errors
- If model appears black: Try switching to "Points View"
- If performance is slow: Enable adaptive streaming

#### Test 1.2: File Format Validation
**Objective:** Test error handling for invalid files

**Steps:**
1. Try loading non-VTP files (`.txt`, `.jpg`, etc.)
2. Try loading corrupted VTP files

**Expected Results:**
- ✅ Error message: "Failed to load VTP file"
- ✅ Log shows: "Make sure the file is a valid VTP format"
- ✅ Application remains stable

### 2. **Dimensionality Reduction Testing**

#### Test 2.1: PCA (Principal Component Analysis)
**Objective:** Test TensorFlow.js-based PCA implementation

**Steps:**
1. Load a VTP file with substantial data (e.g., `Lungs.vtp`)
2. Select "PCA (TensorFlow.js)" from method dropdown
3. Choose "PCA to 3D (reorder axes)" or "PCA to 2D"
4. Click "Toggle Reduction"

**Expected Results:**
- ✅ Log shows: "Starting PCA on X points"
- ✅ Processing completes successfully
- ✅ Visualization updates with transformed data
- ✅ Memory usage tracked and displayed
- ✅ Performance: Should complete within 5-10 seconds for typical datasets

**Performance Benchmarks:**
- Small datasets (< 1K points): < 2 seconds
- Medium datasets (1K-10K points): 2-10 seconds
- Large datasets (10K+ points): 10-30 seconds

#### Test 2.2: t-SNE (t-Distributed Stochastic Neighbor Embedding)
**Objective:** Test pure JavaScript t-SNE implementation

**Steps:**
1. Load a VTP file
2. Select "t-SNE (TensorFlow.js)" from method dropdown
3. Choose "t-SNE to 2D (recommended)"
4. Click "Toggle Reduction"

**Expected Results:**
- ✅ Log shows: "Starting t-SNE on X points"
- ✅ Progress updates during optimization
- ✅ 2D visualization with orthographic projection
- ✅ Clustering patterns visible in 2D space

**Performance Notes:**
- t-SNE is computationally intensive
- Large datasets (> 1K points) are automatically subsampled
- Processing time: 30 seconds to 5 minutes depending on dataset size

#### Test 2.3: UMAP (Uniform Manifold Approximation and Projection)
**Objective:** Test TensorFlow.js-based UMAP implementation

**Steps:**
1. Load a VTP file
2. Select "UMAP (TensorFlow.js)" from method dropdown
3. Adjust parameters:
   - Neighbors: 8 (default)
   - Min Dist: 0.1 (default)
4. Choose "UMAP to 2D (recommended)"
5. Click "Toggle Reduction"

**Expected Results:**
- ✅ Log shows: "Starting TensorFlow.js UMAP on X points"
- ✅ TensorFlow.js operations complete successfully
- ✅ 2D/3D visualization with preserved local and global structure
- ✅ Faster than t-SNE for large datasets

### 3. **Real-time Collaboration Testing**

#### Test 3.1: Multi-Tab Synchronization
**Objective:** Test Yjs-based real-time collaboration

**Steps:**
1. Open two browser tabs to `http://localhost:8080`
2. Load a VTP file in Tab 1
3. Observe Tab 2 automatically loads the same file
4. Rotate/zoom the model in Tab 1
5. Observe Tab 2 updates in real-time

**Expected Results:**
- ✅ File loading syncs across tabs
- ✅ Camera movements sync in real-time
- ✅ Model rotations sync across tabs
- ✅ Representation changes (Points/Surface) sync
- ✅ Dimensionality reduction states sync

#### Test 3.2: WebSocket Connection Testing
**Objective:** Verify WebSocket server functionality

**Steps:**
1. Check WebSocket server is running on port 9001
2. Open browser developer tools → Network tab
3. Look for WebSocket connection to `ws://localhost:9001`
4. Test with multiple browser tabs

**Expected Results:**
- ✅ WebSocket connection established
- ✅ Real-time data synchronization
- ✅ No connection errors in console

### 4. **WebXR/VR Testing**

#### Test 4.1: VR Mode Activation
**Objective:** Test WebXR VR functionality

**Prerequisites:**
- Chrome/Edge browser
- VR headset connected
- WebXR enabled in browser

**Steps:**
1. Load a VTP file
2. Click "Send To VR" button
3. Put on VR headset
4. Navigate in VR space

**Expected Results:**
- ✅ VR session starts successfully
- ✅ 3D model visible in VR space
- ✅ Controller interactions work
- ✅ "Return From VR" button appears

#### Test 4.2: WebXR Emulator Testing
**Objective:** Test VR functionality without physical headset

**Steps:**
1. Install [Immersive Web Emulator Extension](https://chromewebstore.google.com/detail/immersive-web-emulator/cgffilbpcibhmcfbgggfhfolhkfbhmik)
2. Open Chrome DevTools → WebXR tab
3. Enable emulator
4. Click "Send To VR"

**Expected Results:**
- ✅ VR emulator activates
- ✅ Simulated VR environment
- ✅ Mouse controls for VR navigation

### 5. **Adaptive Streaming & Performance Testing**

#### Test 5.1: Network Quality Adaptation
**Objective:** Test adaptive streaming based on network conditions

**Steps:**
1. Load a large VTP file
2. Open browser DevTools → Network tab
3. Throttle network to "Slow 3G"
4. Observe adaptive quality adjustments

**Expected Results:**
- ✅ Network quality display updates
- ✅ Streaming quality adjusts automatically
- ✅ Performance stats show current FPS
- ✅ Memory usage tracked

#### Test 5.2: Viewport Culling
**Objective:** Test frustum culling optimization

**Steps:**
1. Load a complex VTP file
2. Toggle "Viewport Culling" button
3. Rotate camera to different angles
4. Observe culling statistics

**Expected Results:**
- ✅ Culling statistics displayed
- ✅ Performance improvement with culling enabled
- ✅ Objects outside viewport are culled

#### Test 5.3: Level of Detail (LOD) System
**Objective:** Test LOD-based performance optimization

**Steps:**
1. Load a large dataset
2. Toggle "LOD System" button
3. Move camera closer/farther from objects
4. Observe LOD level changes

**Expected Results:**
- ✅ LOD distribution statistics
- ✅ Quality adjusts based on distance
- ✅ Performance improvement for distant objects

### 6. **Memory Management Testing**

#### Test 6.1: TensorFlow.js Memory Management
**Objective:** Test automatic memory cleanup

**Steps:**
1. Load a VTP file
2. Apply PCA reduction multiple times
3. Click "Memory Status & Cleanup"
4. Observe memory usage

**Expected Results:**
- ✅ Memory usage tracked
- ✅ Automatic cleanup after operations
- ✅ No memory leaks detected
- ✅ Tensor count remains reasonable

#### Test 6.2: Large Dataset Handling
**Objective:** Test performance with large datasets

**Steps:**
1. Load the largest available VTP file
2. Apply dimensionality reduction
3. Monitor memory usage and performance
4. Test with multiple browser tabs

**Expected Results:**
- ✅ Automatic subsampling for large datasets
- ✅ Memory usage stays within limits
- ✅ Performance remains acceptable
- ✅ No browser crashes

### 7. **User Interface Testing**

#### Test 7.1: Control Panel Functionality
**Objective:** Test all UI controls

**Steps:**
1. Test method selection dropdown
2. Test components selection
3. Test toggle buttons
4. Test parameter inputs

**Expected Results:**
- ✅ All controls respond correctly
- ✅ Parameter changes take effect
- ✅ UI updates reflect current state
- ✅ No JavaScript errors

#### Test 7.2: Visual Mode Switching
**Objective:** Test different visualization modes

**Steps:**
1. Switch between "Points View" and "Surface View"
2. Test "Force 2D View" functionality
3. Test representation changes

**Expected Results:**
- ✅ Smooth transitions between modes
- ✅ 2D view locks to orthographic projection
- ✅ 3D view restores perspective projection
- ✅ Visual quality appropriate for each mode

### 8. **Error Handling & Edge Cases**

#### Test 8.1: Network Disconnection
**Objective:** Test behavior when network is lost

**Steps:**
1. Load application
2. Disconnect network
3. Try to load files or apply reductions
4. Reconnect network

**Expected Results:**
- ✅ Graceful degradation
- ✅ Error messages for network issues
- ✅ Recovery when network restored
- ✅ No application crashes

#### Test 8.2: Browser Compatibility
**Objective:** Test across different browsers

**Browsers to Test:**
- Chrome (recommended)
- Edge
- Firefox
- Safari

**Expected Results:**
- ✅ Core functionality works in all browsers
- ✅ WebXR features work in supported browsers
- ✅ Performance acceptable across browsers
- ✅ No browser-specific errors

### 9. **Performance Benchmarking**

#### Test 9.1: Load Testing
**Objective:** Test with multiple concurrent users

**Steps:**
1. Open 5+ browser tabs
2. Load different VTP files simultaneously
3. Apply dimensionality reductions
4. Monitor server performance

**Expected Results:**
- ✅ All tabs remain responsive
- ✅ WebSocket server handles multiple connections
- ✅ Memory usage stays reasonable
- ✅ No performance degradation

#### Test 9.2: Stress Testing
**Objective:** Test with very large datasets

**Steps:**
1. Create or obtain very large VTP files (> 100K points)
2. Apply all reduction methods
3. Monitor performance metrics

**Expected Results:**
- ✅ Automatic optimization kicks in
- ✅ Processing completes successfully
- ✅ Memory usage controlled
- ✅ User experience remains smooth

---

## 🔧 Troubleshooting Guide

### Common Issues & Solutions

#### Issue: "Failed to load VTP file"
**Causes:**
- Invalid file format
- Corrupted file
- Browser security restrictions

**Solutions:**
- Verify file is valid VTP format
- Try different VTP file
- Check browser console for specific errors

#### Issue: "TensorFlow.js initialization failed"
**Causes:**
- WebGL not supported
- Browser compatibility issues
- Memory constraints

**Solutions:**
- Use supported browser (Chrome/Edge)
- Enable hardware acceleration
- Close other browser tabs

#### Issue: "WebSocket connection failed"
**Causes:**
- WebSocket server not running
- Port conflicts
- Firewall restrictions

**Solutions:**
- Ensure `node server.js` is running
- Check port 9001 is available
- Verify firewall settings

#### Issue: "VR not working"
**Causes:**
- WebXR not supported
- VR headset not connected
- Browser permissions

**Solutions:**
- Use Chrome/Edge with WebXR support
- Install WebXR emulator extension
- Check VR headset connection

#### Issue: "Performance is slow"
**Causes:**
- Large dataset
- Insufficient hardware
- Network issues

**Solutions:**
- Enable adaptive streaming
- Use smaller datasets
- Check network connection
- Close other applications

---

## 📊 Performance Metrics

### Expected Performance Benchmarks

| Dataset Size | PCA Time | t-SNE Time | UMAP Time | Memory Usage |
|--------------|----------|------------|-----------|--------------|
| < 1K points | < 2s     | < 10s      | < 5s      | < 50MB      |
| 1K-10K points| 2-10s    | 30s-2min  | 10-30s    | 50-200MB    |
| 10K-50K points| 10-30s   | 2-10min   | 30s-2min  | 200-500MB   |
| > 50K points | 30s+     | Subsampled | Subsampled| 500MB+      |

### Quality Metrics

- **Frame Rate:** 30-60 FPS target
- **Memory Usage:** < 1GB for typical datasets
- **Network Latency:** < 100ms for real-time sync
- **Processing Accuracy:** > 95% for dimensionality reduction

---

## 🎯 Testing Checklist

### Pre-Testing Setup
- [ ] Node.js installed (v16+)
- [ ] Dependencies installed (`npm install`)
- [ ] WebSocket server running (`node server.js`)
- [ ] Development server running (`npm start`)
- [ ] Browser with WebXR support
- [ ] Sample VTP files available

### Core Functionality
- [ ] File loading works
- [ ] 3D visualization renders
- [ ] PCA reduction works
- [ ] t-SNE reduction works
- [ ] UMAP reduction works
- [ ] Real-time collaboration works
- [ ] VR mode activates
- [ ] Adaptive streaming works

### Performance Testing
- [ ] Small datasets (< 1K points)
- [ ] Medium datasets (1K-10K points)
- [ ] Large datasets (10K+ points)
- [ ] Multiple browser tabs
- [ ] Memory usage monitoring
- [ ] Network throttling

### Error Handling
- [ ] Invalid file formats
- [ ] Network disconnection
- [ ] Browser compatibility
- [ ] Memory constraints
- [ ] WebSocket failures

### User Experience
- [ ] UI controls responsive
- [ ] Visual feedback clear
- [ ] Error messages helpful
- [ ] Performance acceptable
- [ ] Features intuitive

---

## 📝 Test Report Template

### Test Environment
- **Browser:** [Chrome/Edge/Firefox/Safari]
- **OS:** [Windows/macOS/Linux]
- **Hardware:** [CPU/RAM/GPU specs]
- **Network:** [Connection speed]

### Test Results
- **File Loading:** ✅/❌
- **PCA:** ✅/❌
- **t-SNE:** ✅/❌
- **UMAP:** ✅/❌
- **Collaboration:** ✅/❌
- **VR Support:** ✅/❌
- **Performance:** ✅/❌

### Issues Found
- [List any bugs or issues discovered]

### Recommendations
- [Suggestions for improvements]

---

## 🚀 Advanced Testing Scenarios

### Scenario 1: Scientific Data Analysis
1. Load medical imaging data (Lungs.vtp)
2. Apply PCA to identify principal components
3. Use t-SNE to find clusters
4. Analyze results in VR for immersive exploration

### Scenario 2: Collaborative Research
1. Multiple researchers load same dataset
2. Each applies different reduction methods
3. Compare results in real-time
4. Share insights through synchronized views

### Scenario 3: Educational Use
1. Load anatomical data (Bones.vtp, Skull.vtp)
2. Switch between different visualization modes
3. Apply 2D reductions for easier understanding
4. Use VR for immersive learning

### Scenario 4: Performance Optimization
1. Load largest available dataset
2. Enable all optimization features
3. Monitor performance metrics
4. Test with network throttling
5. Verify memory management

---

This comprehensive testing guide ensures that all aspects of the CIA_Web application are thoroughly tested, from basic functionality to advanced performance scenarios. The guide provides clear steps, expected results, and troubleshooting information to help users and developers verify the application's capabilities.
