# 🔄 Adaptive Streaming Workflow - Logic, Metrics & Decision Making

**Complete Guide to How Adaptive Streaming Works**

---

## 🎯 **Overview: The Adaptive Streaming Process**

The adaptive streaming system uses a **sophisticated weighted scoring algorithm** that evaluates multiple performance metrics and makes intelligent decisions about quality optimization. Here's how it works:

```
📊 Metrics Collection → 🧮 Weighted Scoring → 🎯 Quality Decision → ⚙️ Optimization Application
```

---

## 📊 **Step 1: Metrics Collection**

### **Network Quality Assessment**
```javascript
function getNetworkQuality() {
  const speed = networkMonitor.actualSpeed; // Measured in Mbps
  
  if (speed >= 10) return 'high';        // 100 points
  else if (speed >= 5) return 'medium';   // 70 points  
  else if (speed >= 2) return 'low';      // 40 points
  else return 'very-low';                 // 20 points
}
```

**How it works:**
- **Real-time speed testing** using browser APIs
- **Automatic fallback** to estimation if testing fails
- **Quality classification** based on actual measured speeds
- **Latency monitoring** for additional context

### **FPS Performance Monitoring**
```javascript
function getFPSScore(fpsRatio) {
  const ratio = adaptiveStreaming.currentFPS / adaptiveStreaming.targetFPS;
  
  if (ratio >= 0.9) return 100;  // 90%+ of target = 100 points
  if (ratio >= 0.7) return 70;   // 70-90% of target = 70 points
  if (ratio >= 0.5) return 40;   // 50-70% of target = 40 points
  return 20;                     // <50% of target = 20 points
}
```

**How it works:**
- **Frame counting** every 60 frames for accurate FPS
- **Target comparison** against desired performance (60 FPS default)
- **Ratio calculation** for consistent scoring
- **Real-time updates** every second

### **Memory Usage Tracking**
```javascript
function getMemoryScore(memoryUsage) {
  const usage = getMemoryUsageRatio(); // 0.0 to 1.0
  
  if (usage < 0.5) return 100;   // <50% usage = 100 points
  if (usage < 0.7) return 70;    // 50-70% usage = 70 points
  if (usage < 0.85) return 40;  // 70-85% usage = 40 points
  return 20;                     // >85% usage = 20 points
}
```

**How it works:**
- **Browser memory API** for accurate usage tracking
- **Percentage calculation** relative to available memory
- **Threshold-based scoring** for consistent evaluation
- **Automatic cleanup** when memory is high

---

## 🧮 **Step 2: Weighted Scoring Algorithm**

### **The Core Scoring Logic**
```javascript
function adjustStreamingQuality() {
  // Collect all metrics
  const networkQuality = getNetworkQuality();
  const fpsRatio = adaptiveStreaming.currentFPS / adaptiveStreaming.targetFPS;
  const memoryUsage = getMemoryUsageRatio();
  
  // Calculate individual scores (0-100)
  const networkScore = getNetworkScore(networkQuality);
  const fpsScore = getFPSScore(fpsRatio);
  const memoryScore = getMemoryScore(memoryUsage);
  
  // Apply configurable weights
  const overallScore = (networkScore * adaptiveWeights.network) + 
                      (fpsScore * adaptiveWeights.fps) + 
                      (memoryScore * adaptiveWeights.memory);
  
  // Determine quality level
  let newQuality;
  if (overallScore >= 80) newQuality = 'high';
  else if (overallScore >= 60) newQuality = 'medium';
  else newQuality = 'low';
}
```

### **Why Weighted Scoring is Better**

**❌ Old Logic (Lowest Common Denominator):**
```javascript
// BAD: If ANY metric is poor, quality = low
if (networkQuality === 'low' || fpsRatio < 0.5 || memoryUsage > 0.8) {
  newQuality = 'low';  // Too aggressive!
}
```

**✅ New Logic (Weighted Average):**
```javascript
// GOOD: Consider all factors proportionally
const overallScore = (networkScore * 0.4) +    // Network importance
                    (fpsScore * 0.3) +          // FPS importance  
                    (memoryScore * 0.3);        // Memory importance
```

### **Real-World Example:**
```
Scenario: Fast internet + Slow computer + High memory usage

Network: 'high' (100 points × 40% = 40 points)
FPS: 0.4 ratio (40 points × 30% = 12 points)  
Memory: 0.9 usage (20 points × 30% = 6 points)

Total Score: 40 + 12 + 6 = 58 points
Result: MEDIUM quality (fair and balanced!)
```

---

## 🎯 **Step 3: Quality Decision Making**

### **Quality Level Thresholds**
```javascript
// Quality determination based on overall score
if (overallScore >= 80) {
  newQuality = 'high';     // Excellent conditions
} else if (overallScore >= 60) {
  newQuality = 'medium';   // Mixed conditions
} else {
  newQuality = 'low';      // Poor conditions
}
```

### **Decision Logic Explanation**

| Score Range | Quality Level | Conditions | Optimization Strategy |
|-------------|---------------|------------|---------------------|
| **80-100** | **HIGH** | Excellent network, FPS, and memory | Enable all features, 60 FPS target |
| **60-79** | **MEDIUM** | Mixed conditions, some bottlenecks | Selective optimization, 45 FPS target |
| **0-59** | **LOW** | Poor conditions, multiple bottlenecks | Essential features only, 30 FPS target |

---

## ⚙️ **Step 4: Optimization Application**

### **Component-Specific Optimization**
```javascript
function applyStreamingQuality(quality) {
  switch (quality) {
    case 'high':
      // Enable all optimizations
      viewportCuller.enabled = true;
      lodSystem.enabled = true;
      gazePredictor.enabled = true;
      adaptiveStreaming.targetFPS = 60;
      break;
      
    case 'medium':
      // Selective optimization
      viewportCuller.enabled = true;
      lodSystem.enabled = true;
      gazePredictor.enabled = (networkQuality === 'high' && fpsRatio > 0.8);
      adaptiveStreaming.targetFPS = 45;
      break;
      
    case 'low':
      // Essential features only
      viewportCuller.enabled = true;
      lodSystem.enabled = (memoryUsage > 0.7 || fpsRatio < 0.7);
      gazePredictor.enabled = false;
      adaptiveStreaming.targetFPS = 30;
      break;
  }
}
```

### **Smart Context-Aware Optimization**
```javascript
function smartAdaptiveStreaming() {
  // Auto-adjust weights based on current bottlenecks
  adjustWeightsBasedOnContext();
  
  const metrics = {
    network: getNetworkQuality(),
    fps: adaptiveStreaming.currentFPS,
    memory: getMemoryUsageRatio()
  };
  
  // Different strategies for different scenarios
  if (metrics.network === 'high' && metrics.fps > 50) {
    enableAllOptimizations();           // High performance mode
  } else if (metrics.network === 'low' && metrics.memory > 0.8) {
    enableBandwidthOptimization();     // Bandwidth constrained
  } else if (metrics.fps < 30) {
    enablePerformanceOptimization();  // Performance critical
  } else {
    enableBalancedOptimization();      // Balanced approach
  }
}
```

---

## 🧠 **Step 5: Context-Aware Weight Adjustment**

### **Automatic Weight Optimization**
```javascript
function adjustWeightsBasedOnContext() {
  const networkQuality = getNetworkQuality();
  const fpsRatio = adaptiveStreaming.currentFPS / adaptiveStreaming.targetFPS;
  const memoryUsage = getMemoryUsageRatio();
  
  // If network is poor, prioritize network optimization
  if (networkQuality === 'low' || networkQuality === 'very-low') {
    setAdaptiveWeights({ 
      network: 0.5,    // Increase network weight to 50%
      fps: 0.25,       // Reduce FPS weight to 25%
      memory: 0.25     // Reduce memory weight to 25%
    });
  }
  
  // If FPS is poor, prioritize FPS optimization  
  else if (fpsRatio < 0.5) {
    setAdaptiveWeights({ 
      network: 0.3,    // Reduce network weight to 30%
      fps: 0.5,        // Increase FPS weight to 50%
      memory: 0.2      // Reduce memory weight to 20%
    });
  }
  
  // If memory is high, prioritize memory optimization
  else if (memoryUsage > 0.8) {
    setAdaptiveWeights({ 
      network: 0.3,    // Reduce network weight to 30%
      fps: 0.2,        // Reduce FPS weight to 20%
      memory: 0.5      // Increase memory weight to 50%
    });
  }
}
```

### **Weight Adjustment Logic**

| Bottleneck | Network Weight | FPS Weight | Memory Weight | Strategy |
|------------|----------------|------------|---------------|----------|
| **Poor Network** | 50% | 25% | 25% | Focus on data reduction |
| **Poor FPS** | 30% | 50% | 20% | Focus on rendering optimization |
| **High Memory** | 30% | 20% | 50% | Focus on memory management |
| **Balanced** | 40% | 30% | 30% | Equal consideration |

---

## 🔄 **Step 6: Continuous Monitoring & Updates**

### **Real-Time Monitoring Loop**
```javascript
// Main monitoring loop (runs every second)
setInterval(() => {
  if (!adaptiveStreaming.enabled) return;
  
  // Collect current metrics
  const networkQuality = getNetworkQuality();
  const fpsRatio = adaptiveStreaming.currentFPS / adaptiveStreaming.targetFPS;
  const memoryUsage = getMemoryUsageRatio();
  
  // Calculate scores
  const networkScore = getNetworkScore(networkQuality);
  const fpsScore = getFPSScore(fpsRatio);
  const memoryScore = getMemoryScore(memoryUsage);
  
  // Apply weighted scoring
  const overallScore = (networkScore * adaptiveWeights.network) + 
                      (fpsScore * adaptiveWeights.fps) + 
                      (memoryScore * adaptiveWeights.memory);
  
  // Make quality decision
  let newQuality;
  if (overallScore >= 80) newQuality = 'high';
  else if (overallScore >= 60) newQuality = 'medium';
  else newQuality = 'low';
  
  // Apply optimizations if quality changed
  if (newQuality !== adaptiveStreaming.qualityLevel) {
    applyStreamingQuality(newQuality);
    adaptiveStreaming.qualityLevel = newQuality;
    
    // Show visual feedback
    showQualityChange(newQuality);
  }
}, 1000);
```

### **Visual Feedback System**
```javascript
function showQualityChange(newQuality) {
  // Create floating notification
  const qualityIndicator = document.createElement('div');
  qualityIndicator.style.cssText = `
    position: fixed;
    top: 20px;
    right: 20px;
    background: ${newQuality === 'high' ? '#4CAF50' : 
                 newQuality === 'medium' ? '#FF9800' : '#f44336'};
    color: white;
    padding: 10px 15px;
    border-radius: 5px;
    font-weight: bold;
    z-index: 1000;
  `;
  qualityIndicator.textContent = `🎯 Quality: ${newQuality.toUpperCase()}`;
  document.body.appendChild(qualityIndicator);
  
  // Auto-remove after 3 seconds
  setTimeout(() => {
    if (qualityIndicator.parentNode) {
      qualityIndicator.parentNode.removeChild(qualityIndicator);
    }
  }, 3000);
}
```

---

## 📊 **Step 7: Performance Metrics & Debugging**

### **Comprehensive Metrics Display**
```javascript
function updatePerformanceMetrics() {
  const metrics = {
    quality: adaptiveStreaming.qualityLevel,
    fps: adaptiveStreaming.currentFPS,
    network: getNetworkQuality(),
    memory: getMemoryUsageRatio(),
    weights: adaptiveWeights,
    optimizations: getActiveOptimizations()
  };
  
  // Console logging for debugging
  console.log('📊 Performance Metrics:', {
    'Quality Level': metrics.quality,
    'FPS': `${metrics.fps.toFixed(1)}/${adaptiveStreaming.targetFPS}`,
    'Network': metrics.network,
    'Memory': `${(metrics.memory * 100).toFixed(1)}%`,
    'Weights': `Network(${metrics.weights.network.toFixed(2)}) FPS(${metrics.weights.fps.toFixed(2)}) Memory(${metrics.weights.memory.toFixed(2)})`,
    'Active Optimizations': metrics.optimizations.join(', ')
  });
}
```

### **Real-Time Weight Display**
```javascript
function updateWeightsDisplay() {
  const weightsDisplay = document.getElementById('adaptive-weights-display');
  if (weightsDisplay) {
    weightsDisplay.innerHTML = `
      🎯 Current Weights:<br>
      Network: ${(adaptiveWeights.network * 100).toFixed(0)}% | 
      FPS: ${(adaptiveWeights.fps * 100).toFixed(0)}% | 
      Memory: ${(adaptiveWeights.memory * 100).toFixed(0)}%
    `;
  }
}
```

---

## 🎯 **Decision Making Flowchart**

```
📊 Collect Metrics
    ↓
🧮 Calculate Scores (Network, FPS, Memory)
    ↓
⚖️ Apply Weights (Configurable: 40%, 30%, 30%)
    ↓
🧮 Calculate Overall Score (0-100)
    ↓
🎯 Determine Quality Level
    ├─ Score ≥ 80 → HIGH quality
    ├─ Score ≥ 60 → MEDIUM quality  
    └─ Score < 60 → LOW quality
    ↓
⚙️ Apply Optimizations
    ├─ HIGH: All features enabled
    ├─ MEDIUM: Selective optimization
    └─ LOW: Essential features only
    ↓
📊 Monitor & Update (Every 1 second)
```

---

## 🔧 **Configuration Options**

### **Weight Presets**
```javascript
// Balanced (Default)
setBalancedWeights();        // Network(40%), FPS(30%), Memory(30%)

// Network Focus
setNetworkConstrainedWeights(); // Network(60%), FPS(20%), Memory(20%)

// Performance Focus  
setHighPerformanceWeights();    // Network(30%), FPS(40%), Memory(30%)

// Mobile Optimized
setMobileWeights();             // Network(40%), FPS(30%), Memory(30%)
```

### **Smart Mode Features**
- **Context-Aware Optimization**: Different strategies for different scenarios
- **Automatic Weight Adjustment**: Dynamic weight changes based on bottlenecks
- **Intelligent Feature Selection**: Enable only relevant optimizations
- **Performance-Based Adaptation**: Quality adjustment based on real-time metrics

---

## 🎉 **Key Benefits of This Approach**

### **✅ Intelligent Decision Making**
- **No Over-Reaction**: System doesn't degrade unnecessarily
- **Fair Assessment**: Considers all factors proportionally
- **Context-Aware**: Automatically adjusts based on situation
- **Better User Experience**: Smoother quality transitions

### **✅ Flexible Configuration**
- **Configurable Weights**: Easy adjustment for different scenarios
- **Smart Mode**: Automatic weight optimization
- **Preset Configurations**: Quick setup for common use cases
- **Real-time Monitoring**: Transparent system operation

### **✅ Performance Optimization**
- **Component-Specific**: Only enable relevant optimizations
- **Resource Efficient**: Smart feature selection
- **Adaptive**: Responds to changing conditions
- **Visual Feedback**: Users understand system decisions

**This workflow makes the adaptive streaming system intelligent, fair, and user-friendly!** 🚀
