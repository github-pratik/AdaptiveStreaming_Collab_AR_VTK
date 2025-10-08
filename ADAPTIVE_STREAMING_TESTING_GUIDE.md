# 🧪 Adaptive Streaming Testing Guide

**Comprehensive Testing Guide for Adaptive Streaming Implementation in CIA_Web**

This guide focuses specifically on testing the adaptive streaming features, ML-powered optimizations, and performance enhancements implemented in the CIA_Web platform.

---

## 🚀 **Quick Start for Adaptive Streaming Testing**

### **Prerequisites**
- Node.js (v16+)
- Modern browser (Chrome/Edge recommended)
- Network throttling capability (Chrome DevTools)
- Large VTP datasets for stress testing

### **Setup for Testing**
```bash
# Terminal 1: Start WebSocket server
node server.js

# Terminal 2: Start development server
npm start
```

**Access Points:**
- **Main App:** http://localhost:8080
- **WebSocket:** ws://localhost:9001

---

## 📊 **Adaptive Streaming Core Tests**

### **Test 1: Network Bandwidth Monitoring**

#### **Test 1.1: Network Quality Detection**
**Objective:** Verify real-time network quality monitoring

**Steps:**
1. Open http://localhost:8080
2. Load a VTP file (e.g., `Lungs.vtp`)
3. Observe the "Network Quality Display" in the control panel
4. Check browser console for network monitoring logs

**Expected Results:**
- ✅ Network quality displayed: "HIGH", "MEDIUM", "LOW", or "VERY-LOW"
- ✅ Bandwidth value shown in Mbps
- ✅ Log shows: "Network monitoring initialized"
- ✅ Real-time updates every 2 seconds

**Test Network Conditions:**
```javascript
// Test different network speeds in Chrome DevTools
// Network tab → Throttling → Select:
// - Fast 3G (1.6 Mbps)
// - Slow 3G (0.4 Mbps)  
// - Offline
```

#### **Test 1.2: Network Adaptation**
**Objective:** Test automatic quality adjustment based on network

**Steps:**
1. Load a large VTP file
2. Enable "Adaptive Streaming" toggle
3. Throttle network to "Slow 3G"
4. Observe quality adjustment
5. Restore to "Fast 3G"
6. Watch quality improve

**Expected Results:**
- ✅ Quality automatically decreases on slow network
- ✅ Quality automatically increases on fast network
- ✅ Log shows: "Streaming quality adjusted: [quality]"
- ✅ Performance stats update accordingly

---

### **Test 2: Viewport Culling (Frustum Culling)**

#### **Test 2.1: Culling Activation**
**Objective:** Test viewport culling system activation

**Steps:**
1. Load a complex VTP file (e.g., `Lungs.vtp`)
2. Enable "Toggle Viewport Culling" button
3. Rotate camera to different angles
4. Observe culling statistics in logs

**Expected Results:**
- ✅ Button shows "Viewport Culling: ON"
- ✅ Log shows: "Viewport culling: X/Y objects visible (Z% culled)"
- ✅ Performance improvement with culling enabled
- ✅ Objects outside viewport are hidden

#### **Test 2.2: Culling Performance**
**Objective:** Measure culling performance impact

**Steps:**
1. Load large dataset (10K+ points)
2. Disable viewport culling
3. Record FPS in performance stats
4. Enable viewport culling
5. Compare FPS improvement

**Expected Results:**
- ✅ 60-80% bandwidth reduction with culling
- ✅ FPS improvement of 20-40%
- ✅ Culling ratio displayed in logs
- ✅ Smooth camera movement with culling

#### **Test 2.3: Culling Toggle**
**Objective:** Test manual culling control

**Steps:**
1. Load VTP file
2. Toggle "Viewport Culling" on/off multiple times
3. Observe visual changes
4. Check performance stats

**Expected Results:**
- ✅ All objects visible when culling disabled
- ✅ Selective visibility when culling enabled
- ✅ Performance stats reflect changes
- ✅ Log shows culling status changes

---

### **Test 3: Level of Detail (LOD) System**

#### **Test 3.1: LOD Activation**
**Objective:** Test LOD system initialization

**Steps:**
1. Load a VTP file
2. Enable "Toggle LOD System" button
3. Move camera closer/farther from objects
4. Observe LOD distribution in logs

**Expected Results:**
- ✅ Button shows "LOD System: ON"
- ✅ Log shows: "LOD distribution: Ultra(X) High(Y) Medium(Z)..."
- ✅ Quality changes based on distance
- ✅ Performance improvement for distant objects

#### **Test 3.2: LOD Distance Testing**
**Objective:** Test LOD levels at different distances

**Steps:**
1. Load VTP file with LOD enabled
2. Position camera at different distances:
   - Very close (0-50 units) → Ultra quality
   - Close (50-100 units) → High quality
   - Medium (100-200 units) → Medium quality
   - Far (200-500 units) → Low quality
   - Very far (500+ units) → Very Low quality
3. Observe quality changes

**Expected Results:**
- ✅ Quality automatically adjusts based on distance
- ✅ LOD statistics update in real-time
- ✅ Performance improves with distance
- ✅ Visual quality appropriate for distance

#### **Test 3.3: LOD Performance Impact**
**Objective:** Measure LOD performance benefits

**Steps:**
1. Load large dataset
2. Disable LOD system
3. Record performance metrics
4. Enable LOD system
5. Compare performance improvement

**Expected Results:**
- ✅ 30-50% performance improvement with LOD
- ✅ Reduced memory usage
- ✅ Smoother frame rates
- ✅ LOD statistics displayed

---

### **Test 4: ML-Based Gaze Prediction**

#### **Test 4.1: Gaze Prediction Initialization**
**Objective:** Test ML gaze prediction system startup

**Steps:**
1. Load VTP file
2. Enable "Toggle Gaze Prediction" button
3. Move camera around for 30 seconds
4. Check logs for gaze prediction activity

**Expected Results:**
- ✅ Button shows "Gaze Prediction: ON"
- ✅ Log shows: "Gaze prediction system initialized"
- ✅ Gaze data collection starts
- ✅ TensorFlow.js model loads successfully

#### **Test 4.2: Gaze Data Collection**
**Objective:** Test gaze direction tracking

**Steps:**
1. Enable gaze prediction
2. Move camera in different directions:
   - Up, down, left, right
   - Circular movements
   - Zoom in/out
3. Observe gaze prediction logs

**Expected Results:**
- ✅ Gaze direction tracked: "[x, y, z] coordinates"
- ✅ Log shows: "Gaze prediction: [direction]"
- ✅ Pre-fetching triggered for predicted areas
- ✅ Smooth prediction updates

#### **Test 4.3: ML Model Training**
**Objective:** Test LSTM model training

**Steps:**
1. Enable gaze prediction
2. Move camera extensively for 2-3 minutes
3. Check for model training logs
4. Observe prediction accuracy improvement

**Expected Results:**
- ✅ Training data collected (50+ data points)
- ✅ Log shows: "Training gaze prediction model..."
- ✅ Training epochs completed
- ✅ Model accuracy improves over time

---

### **Test 5: Adaptive Streaming Controller**

#### **Test 5.1: Centralized Control**
**Objective:** Test adaptive streaming controller

**Steps:**
1. Load VTP file
2. Enable "Toggle Adaptive Streaming"
3. Monitor all optimization systems
4. Check performance stats

**Expected Results:**
- ✅ Button shows "Adaptive Streaming: ON"
- ✅ All optimization systems coordinated
- ✅ Performance stats display real-time metrics
- ✅ Quality automatically adjusted

#### **Test 5.2: Multi-Factor Optimization**
**Objective:** Test combined optimization factors

**Steps:**
1. Enable adaptive streaming
2. Load large dataset
3. Throttle network to "Slow 3G"
4. Move camera rapidly
5. Observe automatic adjustments

**Expected Results:**
- ✅ Network quality affects streaming
- ✅ FPS monitoring triggers adjustments
- ✅ Memory usage influences quality
- ✅ All factors combined for optimal performance

#### **Test 5.3: Quality Level Changes**
**Objective:** Test automatic quality level adjustment

**Steps:**
1. Start with high-quality settings
2. Gradually reduce network speed
3. Observe quality level changes
4. Restore network speed
5. Watch quality improve

**Expected Results:**
- ✅ Quality: HIGH → MEDIUM → LOW based on conditions
- ✅ Log shows: "Streaming quality adjusted: [level]"
- ✅ Performance targets adjusted (60→45→30 FPS)
- ✅ Optimization features enabled/disabled accordingly

---

## 🔧 **Performance Testing**

### **Test 6: Memory Management**

#### **Test 6.1: TensorFlow.js Memory Cleanup**
**Objective:** Test automatic memory management

**Steps:**
1. Load VTP file
2. Apply PCA reduction multiple times
3. Click "Memory Status & Cleanup"
4. Monitor memory usage

**Expected Results:**
- ✅ Memory usage tracked in logs
- ✅ Automatic cleanup after operations
- ✅ Tensor count remains reasonable
- ✅ No memory leaks detected

#### **Test 6.2: Large Dataset Handling**
**Objective:** Test memory optimization with large datasets

**Steps:**
1. Load largest available VTP file
2. Apply dimensionality reduction
3. Monitor memory usage
4. Test with multiple browser tabs

**Expected Results:**
- ✅ Memory usage stays within limits
- ✅ Automatic subsampling for large datasets
- ✅ Performance remains acceptable
- ✅ No browser crashes

### **Test 7: Network Stress Testing**

#### **Test 7.1: Bandwidth Limitation**
**Objective:** Test performance under bandwidth constraints

**Steps:**
1. Set network to "Slow 3G" (0.4 Mbps)
2. Load large VTP file
3. Enable all adaptive streaming features
4. Monitor performance

**Expected Results:**
- ✅ Application remains responsive
- ✅ Quality automatically reduced
- ✅ Culling and LOD systems active
- ✅ Smooth user experience maintained

#### **Test 7.2: Network Recovery**
**Objective:** Test adaptation to network improvements

**Steps:**
1. Start with "Slow 3G" network
2. Load VTP file with adaptive streaming
3. Gradually improve network speed
4. Observe quality improvements

**Expected Results:**
- ✅ Quality automatically increases
- ✅ Performance targets raised
- ✅ More optimization features enabled
- ✅ Smooth transition between quality levels

---

## 🎮 **User Interface Testing**

### **Test 8: Adaptive Streaming Controls**

#### **Test 8.1: Control Panel Integration**
**Objective:** Test all adaptive streaming UI controls

**Steps:**
1. Load VTP file
2. Test each control button:
   - Toggle Adaptive Streaming
   - Toggle Viewport Culling
   - Toggle LOD System
   - Toggle Gaze Prediction
3. Verify status updates

**Expected Results:**
- ✅ All buttons respond correctly
- ✅ Status displays update in real-time
- ✅ Color coding reflects current state
- ✅ No JavaScript errors

#### **Test 8.2: Performance Stats Display**
**Objective:** Test real-time performance monitoring

**Steps:**
1. Enable adaptive streaming
2. Load VTP file
3. Monitor performance stats display
4. Perform various operations

**Expected Results:**
- ✅ FPS displayed in real-time
- ✅ Memory usage percentage shown
- ✅ Network quality indicator
- ✅ Stats update every second

### **Test 9: Real-time Monitoring**

#### **Test 9.1: Logging System**
**Objective:** Test comprehensive logging

**Steps:**
1. Enable all adaptive streaming features
2. Perform various operations
3. Check real-time logging panel
4. Test log controls (hide/show/clear)

**Expected Results:**
- ✅ Color-coded log messages
- ✅ Timestamp for each entry
- ✅ Progress indicators
- ✅ Error/warning highlighting

#### **Test 9.2: Network Quality Display**
**Objective:** Test network monitoring display

**Steps:**
1. Load VTP file
2. Observe network quality display
3. Change network conditions
4. Watch display updates

**Expected Results:**
- ✅ Network quality shown: HIGH/MEDIUM/LOW
- ✅ Bandwidth value displayed
- ✅ Color coding based on quality
- ✅ Updates every 2 seconds

---

## 🚨 **Error Handling & Edge Cases**

### **Test 10: Failure Scenarios**

#### **Test 10.1: Network Disconnection**
**Objective:** Test behavior when network is lost

**Steps:**
1. Load VTP file with adaptive streaming
2. Disconnect network
3. Try to load files or apply reductions
4. Reconnect network

**Expected Results:**
- ✅ Graceful degradation
- ✅ Error messages for network issues
- ✅ Recovery when network restored
- ✅ No application crashes

#### **Test 10.2: ML Model Failure**
**Objective:** Test behavior when ML features fail

**Steps:**
1. Disable JavaScript in browser
2. Try to enable gaze prediction
3. Check error handling
4. Re-enable JavaScript

**Expected Results:**
- ✅ Graceful fallback to non-ML features
- ✅ Error messages for ML failures
- ✅ Application remains functional
- ✅ Other features continue working

#### **Test 10.3: Memory Exhaustion**
**Objective:** Test behavior under memory pressure

**Steps:**
1. Load multiple large VTP files
2. Apply multiple reductions
3. Monitor memory usage
4. Test cleanup mechanisms

**Expected Results:**
- ✅ Automatic memory cleanup
- ✅ Warning messages for high usage
- ✅ Performance degradation handled gracefully
- ✅ No browser crashes

---

## 📊 **Performance Benchmarks**

### **Expected Performance Metrics**

| Test Scenario | Network | FPS Target | Memory Usage | Bandwidth Reduction |
|---------------|---------|------------|--------------|-------------------|
| Small Dataset | Fast 3G | 60 FPS | < 100MB | 20-30% |
| Medium Dataset | Fast 3G | 60 FPS | 100-300MB | 40-60% |
| Large Dataset | Fast 3G | 45 FPS | 300-500MB | 60-80% |
| Small Dataset | Slow 3G | 30 FPS | < 100MB | 60-80% |
| Medium Dataset | Slow 3G | 30 FPS | 100-300MB | 70-85% |
| Large Dataset | Slow 3G | 30 FPS | 300-500MB | 80-90% |

### **Quality Level Thresholds**

| Network Quality | FPS Threshold | Memory Threshold | Quality Level |
|-----------------|---------------|------------------|---------------|
| High (>10 Mbps) | >54 FPS | <70% | HIGH |
| Medium (5-10 Mbps) | >36 FPS | <80% | MEDIUM |
| Low (1-5 Mbps) | >21 FPS | <90% | LOW |
| Very Low (<1 Mbps) | Any | Any | LOW |

---

## 🎯 **Testing Checklist**

### **Pre-Testing Setup**
- [ ] Node.js installed (v16+)
- [ ] Dependencies installed (`npm install`)
- [ ] WebSocket server running (`node server.js`)
- [ ] Development server running (`npm start`)
- [ ] Browser with DevTools access
- [ ] Sample VTP files available

### **Adaptive Streaming Features**
- [ ] Network monitoring works
- [ ] Viewport culling reduces bandwidth
- [ ] LOD system adjusts quality
- [ ] Gaze prediction tracks movement
- [ ] Adaptive controller coordinates all systems
- [ ] Performance stats display correctly

### **Performance Testing**
- [ ] Small datasets (< 1K points)
- [ ] Medium datasets (1K-10K points)
- [ ] Large datasets (10K+ points)
- [ ] Network throttling scenarios
- [ ] Memory management
- [ ] Multi-tab collaboration

### **Error Handling**
- [ ] Network disconnection
- [ ] ML model failures
- [ ] Memory exhaustion
- [ ] Browser compatibility
- [ ] Invalid file formats

### **User Experience**
- [ ] UI controls responsive
- [ ] Real-time monitoring works
- [ ] Performance acceptable
- [ ] Error messages helpful
- [ ] Features intuitive

---

## 📝 **Test Report Template**

### **Test Environment**
- **Browser:** [Chrome/Edge/Firefox/Safari]
- **OS:** [Windows/macOS/Linux]
- **Hardware:** [CPU/RAM/GPU specs]
- **Network:** [Connection speed and type]

### **Adaptive Streaming Test Results**
- **Network Monitoring:** ✅/❌
- **Viewport Culling:** ✅/❌
- **LOD System:** ✅/❌
- **Gaze Prediction:** ✅/❌
- **Adaptive Controller:** ✅/❌
- **Performance Optimization:** ✅/❌

### **Performance Metrics**
- **Bandwidth Reduction:** [X]%
- **FPS Improvement:** [X]%
- **Memory Usage:** [X]MB
- **Network Adaptation:** ✅/❌

### **Issues Found**
- [List any bugs or issues with adaptive streaming]

### **Recommendations**
- [Suggestions for adaptive streaming improvements]

---

## 🚀 **Advanced Testing Scenarios**

### **Scenario 1: Scientific Research**
1. Load medical imaging data (Lungs.vtp)
2. Enable all adaptive streaming features
3. Simulate slow network conditions
4. Test collaborative analysis with multiple users
5. Verify performance under stress

### **Scenario 2: Educational Use**
1. Load anatomical data (Bones.vtp, Skull.vtp)
2. Enable adaptive streaming for classroom use
3. Test with multiple browser tabs
4. Verify smooth experience on various devices
5. Test VR mode with adaptive streaming

### **Scenario 3: Industrial Application**
1. Load large engineering datasets
2. Test with network constraints
3. Verify collaborative features
4. Test performance optimization
5. Validate memory management

### **Scenario 4: Performance Optimization**
1. Load largest available dataset
2. Enable all optimization features
3. Test with network throttling
4. Monitor memory usage
5. Verify adaptive quality adjustment

---

This comprehensive testing guide ensures that all adaptive streaming features are thoroughly tested, from basic functionality to advanced performance scenarios. The guide provides clear steps, expected results, and troubleshooting information to help users and developers verify the adaptive streaming implementation's capabilities.
