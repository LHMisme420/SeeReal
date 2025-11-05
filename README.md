# SeeReal
Deep Fake Detection Drills
reality-check-app/
├── README.md
├── package.json
├── app.json
├── babel.config.js
├── metro.config.js
├── src/
│   ├── components/
│   │   ├── Drill/
│   │   │   ├── DeepfakeDrill.js
│   │   │   ├── FallacyDrill.js
│   │   │   └── SourceCheckDrill.js
│   │   ├── UI/
│   │   │   ├── Button.js
│   │   │   ├── ProgressBar.js
│   │   │   └── Badge.js
│   │   └── Common/
│   │       ├── Header.js
│   │       └── Footer.js
│   ├── screens/
│   │   ├── Onboarding.js
│   │   ├── Dashboard.js
│   │   ├── DrillScreen.js
│   │   ├── ProgressScreen.js
│   │   └── ProfileScreen.js
│   ├── data/
│   │   ├── drills.js
│   │   ├── fallacies.js
│   │   └── progressData.js
│   ├── utils/
│   │   ├── storage.js
│   │   ├── helpers.js
│   │   └── constants.js
│   └── styles/
│       ├── colors.js
│       ├── typography.js
│       └── global.js
├── assets/
│   ├── images/
│   ├── videos/
│   └── icons/
└── docs/
    ├── SETUP.md
    └── CONTRIBUTING.md{
  "name": "reality-check",
  "version": "1.0.0",
  "description": "Build your cognitive immune system against AI misinformation",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "expo": "~49.0.0",
    "expo-status-bar": "~1.6.0",
    "react": "18.2.0",
    "react-native": "0.72.0",
    "@react-navigation/native": "^6.1.0",
    "@react-navigation/stack": "^6.3.0",
    "@react-native-async-storage/async-storage": "1.18.0",
    "react-native-safe-area-context": "4.6.0",
    "lottie-react-native": "5.1.0"
  },
  "devDependencies": {
    "@babel/core": "^7.20.0"
  },
  "private": true
}import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { StatusBar } from 'expo-status-bar';

// Screens
import Onboarding from './src/screens/Onboarding';
import Dashboard from './src/screens/Dashboard';
import DrillScreen from './src/screens/DrillScreen';
import ProgressScreen from './src/screens/ProgressScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <StatusBar style="auto" />
      <Stack.Navigator initialRouteName="Onboarding">
        <Stack.Screen 
          name="Onboarding" 
          component={Onboarding}
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="Dashboard" 
          component={Dashboard}
          options={{ title: 'Reality Check' }}
        />
        <Stack.Screen 
          name="DrillScreen" 
          component={DrillScreen}
          options={{ title: 'Daily Drill' }}
        />
        <Stack.Screen 
          name="ProgressScreen" 
          component={ProgressScreen}
          options={{ title: 'Your Progress' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}import React from 'react';
import { View, Text, TouchableOpacity, StyleSheet } from 'react-native';
import { LinearGradient } from 'expo-linear-gradient';

export default function Dashboard({ navigation }) {
  return (
    <View style={styles.container}>
      {/* Streak Header */}
      <LinearGradient
        colors={['#667eea', '#764ba2']}
        style={styles.streakCard}
      >
        <Text style={styles.streakLabel}>🔥 Current Streak</Text>
        <Text style={styles.streakCount}>7 days</Text>
        <Text style={styles.streakSubtitle}>Keep building your cognitive immune system!</Text>
      </LinearGradient>

      {/* Daily Challenge */}
      <View style={styles.challengeCard}>
        <Text style={styles.challengeTitle}>🎯 Today's Challenge</Text>
        <Text style={styles.challengeDescription}>
          Deepfake Detection: Identify AI-generated videos
        </Text>
        
        <TouchableOpacity 
          style={styles.startButton}
          onPress={() => navigation.navigate('DrillScreen')}
        >
          <Text style={styles.startButtonText}>Start Daily Drill</Text>
        </TouchableOpacity>
      </View>

      {/* Quick Stats */}
      <View style={styles.statsContainer}>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>84%</Text>
          <Text style={styles.statLabel}>Accuracy</Text>
        </View>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>23</Text>
          <Text style={styles.statLabel}>Drills Completed</Text>
        </View>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>5</Text>
          <Text style={styles.statLabel}>Badges</Text>
        </View>
      </View>

      {/* Navigation */}
      <TouchableOpacity 
        style={styles.progressButton}
        onPress={() => navigation.navigate('ProgressScreen')}
      >
        <Text style={styles.progressButtonText}>View Full Progress →</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f5f5f5',
  },
  streakCard: {
    padding: 20,
    borderRadius: 15,
    marginBottom: 20,
  },
  streakLabel: {
    color: 'white',
    fontSize: 16,
    marginBottom: 5,
  },
  streakCount: {
    color: 'white',
    fontSize: 32,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  streakSubtitle: {
    color: 'rgba(255,255,255,0.8)',
    fontSize: 14,
  },
  challengeCard: {
    backgroundColor: 'white',
    padding: 20,
    borderRadius: 15,
    marginBottom: 20,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 6,
    elevation: 3,
  },
  challengeTitle: {
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  challengeDescription: {
    fontSize: 16,
    color: '#666',
    marginBottom: 20,
  },
  startButton: {
    backgroundColor: '#4CAF50',
    padding: 15,
    borderRadius: 10,
    alignItems: 'center',
  },
  startButtonText: {
    color: 'white',
    fontSize: 18,
    fontWeight: 'bold',
  },
  statsContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 20,
  },
  stat: {
    backgroundColor: 'white',
    padding: 15,
    borderRadius: 10,
    alignItems: 'center',
    flex: 1,
    marginHorizontal: 5,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.1,
    shadowRadius: 3,
    elevation: 2,
  },
  statNumber: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#333',
  },
  statLabel: {
    fontSize: 12,
    color: '#666',
    marginTop: 5,
  },
  progressButton: {
    padding: 15,
    alignItems: 'center',
  },
  progressButtonText: {
    color: '#667eea',
    fontSize: 16,
    fontWeight: '600',
  },
});import React, { useState } from 'react';
import { View, Text, TouchableOpacity, StyleSheet, Alert } from 'react-native';

export default function DeepfakeDrill({ drill, onComplete }) {
  const [selectedAnswer, setSelectedAnswer] = useState(null);
  const [showFeedback, setShowFeedback] = useState(false);

  const handleAnswer = (answer) => {
    setSelectedAnswer(answer);
    setShowFeedback(true);
    
    // Check if correct
    const isCorrect = answer === drill.correctAnswer;
    
    setTimeout(() => {
      onComplete(isCorrect);
      setShowFeedback(false);
      setSelectedAnswer(null);
    }, 3000);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Deepfake Detection</Text>
      <Text style={styles.question}>Is this video real or AI-generated?</Text>
      
      {/* Video placeholder */}
      <View style={styles.videoPlaceholder}>
        <Text style={styles.videoText}>🎥 Video Player</Text>
        <Text style={styles.videoDescription}>{drill.description}</Text>
      </View>

      {/* Answer Options */}
      {!showFeedback ? (
        <View style={styles.answerContainer}>
          <TouchableOpacity 
            style={styles.answerButton}
            onPress={() => handleAnswer('real')}
          >
            <Text style={styles.answerText}>🤔 Real</Text>
          </TouchableOpacity>
          
          <TouchableOpacity 
            style={styles.answerButton}
            onPress={() => handleAnswer('ai')}
          >
            <Text style={styles.answerText}>🤖 AI-Generated</Text>
          </TouchableOpacity>
        </View>
      ) : (
        <View style={[
          styles.feedbackContainer,
          selectedAnswer === drill.correctAnswer ? styles.correct : styles.incorrect
        ]}>
          <Text style={styles.feedbackEmoji}>
            {selectedAnswer === drill.correctAnswer ? '✅' : '❌'}
          </Text>
          <Text style={styles.feedbackText}>
            {selectedAnswer === drill.correctAnswer ? 'Correct!' : 'Not quite!'}
          </Text>
          <Text style={styles.feedbackDetails}>
            {drill.feedback}
          </Text>
          <Text style={styles.tellTaleSigns}>
            🔍 Tell-tale signs: {drill.tellTaleSigns}
          </Text>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginBottom: 10,
  },
  question: {
    fontSize: 18,
    textAlign: 'center',
    marginBottom: 30,
    color: '#666',
  },
  videoPlaceholder: {
    backgroundColor: '#e0e0e0',
    height: 200,
    borderRadius: 10,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 30,
  },
  videoText: {
    fontSize: 24,
    marginBottom: 10,
  },
  videoDescription: {
    fontSize: 14,
    color: '#666',
    textAlign: 'center',
    paddingHorizontal: 20,
  },
  answerContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  answerButton: {
    flex: 1,
    backgroundColor: 'white',
    padding: 20,
    borderRadius: 10,
    marginHorizontal: 5,
    alignItems: 'center',
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3,
  },
  answerText: {
    fontSize: 16,
    fontWeight: '600',
  },
  feedbackContainer: {
    padding: 20,
    borderRadius: 10,
    alignItems: 'center',
  },
  correct: {
    backgroundColor: '#d4edda',
    borderColor: '#c3e6cb',
  },
  incorrect: {
    backgroundColor: '#f8d7da',
    borderColor: '#f5c6cb',
  },
  feedbackEmoji: {
    fontSize: 32,
    marginBottom: 10,
  },
  feedbackText: {
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  feedbackDetails: {
    fontSize: 16,
    textAlign: 'center',
    marginBottom: 10,
  },
  tellTaleSigns: {
    fontSize: 14,
    fontStyle: 'italic',
    textAlign: 'center',
    color: '#666',
  },
});export const deepfakeDrills = [
  {
    id: 1,
    type: 'deepfake',
    description: 'Political speech by a world leader announcing new policy',
    correctAnswer: 'ai',
    feedback: 'This was an AI-generated deepfake! The subtle facial movements and voice cadence were slightly unnatural.',
    tellTaleSigns: 'Unnatural eye blinking pattern, slight audio sync issues, background artifacts',
    difficulty: 'beginner',
    points: 10
  },
  {
    id: 2,
    type: 'deepfake', 
    description: 'Celebrity endorsement for a financial product',
    correctAnswer: 'ai',
    feedback: 'AI-generated! Celebrities rarely endorse financial products in this manner.',
    tellTaleSigns: 'Overly perfect lighting, repetitive head movements, unnatural smile timing',
    difficulty: 'beginner',
    points: 10
  },
  {
    id: 3,
    type: 'deepfake',
    description: 'News report about a natural disaster with emergency instructions',
    correctAnswer: 'real',
    feedback: 'This was real footage from verified news sources.',
    tellTaleSigns: 'Consistent background noise, natural camera movements, verified source logos',
    difficulty: 'beginner',
    points: 10
  }
];

export const fallacyDrills = [
  {
    id: 1,
    type: 'fallacy',
    text: 'This new AI technology will either save humanity or destroy it completely. There is no middle ground.',
    correctFallacy: 'false-dilemma',
    options: ['false-dilemma', 'appeal-to-emotion', 'ad-hominem', 'straw-man'],
    feedback: 'This is a False Dilemma fallacy - presenting only two extreme options when many possibilities exist.',
    difficulty: 'beginner',
    points: 10
  }
];import AsyncStorage from '@react-native-async-storage/async-storage';

const STORAGE_KEYS = {
  USER_PROGRESS: '@reality_check_user_progress',
  CURRENT_STREAK: '@reality_check_current_streak',
  COMPLETED_DRILLS: '@reality_check_completed_drills',
  BADGES_EARNED: '@reality_check_badges_earned'
};

export const Storage = {
  // Save user progress
  async saveProgress(progress) {
    try {
      await AsyncStorage.setItem(STORAGE_KEYS.USER_PROGRESS, JSON.stringify(progress));
    } catch (error) {
      console.error('Error saving progress:', error);
    }
  },

  // Load user progress
  async loadProgress() {
    try {
      const progress = await AsyncStorage.getItem(STORAGE_KEYS.USER_PROGRESS);
      return progress ? JSON.parse(progress) : {
        totalDrills: 0,
        correctAnswers: 0,
        currentStreak: 0,
        badges: []
      };
    } catch (error) {
      console.error('Error loading progress:', error);
      return null;
    }
  },

  // Update streak
  async updateStreak() {
    try {
      const today = new Date().toDateString();
      const lastCompletion = await AsyncStorage.getItem(STORAGE_KEYS.LAST_COMPLETION);
      
      if (lastCompletion !== today) {
        const currentStreak = parseInt(await AsyncStorage.getItem(STORAGE_KEYS.CURRENT_STREAK) || '0');
        const newStreak = lastCompletion ? currentStreak + 1 : 1;
        
        await AsyncStorage.setItem(STORAGE_KEYS.CURRENT_STREAK, newStreak.toString());
        await AsyncStorage.setItem(STORAGE_KEYS.LAST_COMPLETION, today);
        
        return newStreak;
      }
      return parseInt(await AsyncStorage.getItem(STORAGE_KEYS.CURRENT_STREAK) || '0');
    } catch (error) {
      console.error('Error updating streak:', error);
      return 0;
    }
  }
};# 🛡️ Reality Check - AI Safety Mental Health App

Build your cognitive immune system against AI misinformation with daily critical thinking drills.

## 🎯 Features

- **Daily Deepfake Detection Drills** - Train your eye to spot AI-generated content
- **Logical Fallacy Identification** - Learn to recognize manipulation techniques  
- **Source Verification Training** - Develop healthy skepticism habits
- **Progress Tracking** - Monitor your improvement with detailed analytics
- **Badge System** - Earn rewards for consistent training

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/your-username/reality-check-app.git

# Install dependencies
npm install

# Start the development server
npm start
## 🚀 Next Steps to Run This:

1. **Create new Expo project:**
   ```bash
   npx create-expo-app reality-check
   cd reality-checknpm install @react-navigation/native @react-navigation/stack @react-native-async-storage/async-storage lottie-react-nativenpm start
{
  "name": "reality-check-seereal",
  "version": "2.0.0",
  "description": "AI Safety Suite: Deepfake detection + critical thinking training",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android", 
    "ios": "expo start --ios",
    "web": "expo start --web",
    "detection-train": "python scripts/train_detector.py"
  },
  "dependencies": {
    "expo": "~49.0.0",
    "expo-status-bar": "~1.6.0",
    "expo-camera": "~13.4.0",
    "expo-image-picker": "~14.3.0",
    "react": "18.2.0",
    "react-native": "0.72.0",
    "@react-navigation/native": "^6.1.0",
    "@react-navigation/stack": "^6.3.0",
    "@react-native-async-storage/async-storage": "1.18.0",
    "@tensorflow/tfjs-react-native": "^0.8.0",
    "@tensorflow/tfjs": "^4.11.0",
    "lottie-react-native": "5.1.0"
  },
  "devDependencies": {
    "@babel/core": "^7.20.0"
  }
}import React, { useState, useRef } from 'react';
import { View, Text, TouchableOpacity, StyleSheet, Alert } from 'react-native';
import { Camera } from 'expo-camera';
import * as ImagePicker from 'expo-image-picker';

export default function SeeRealDetector({ onAnalysisComplete }) {
  const [hasPermission, setHasPermission] = useState(null);
  const [type, setType] = useState(Camera.Constants.Type.back);
  const [analyzing, setAnalyzing] = useState(false);
  const cameraRef = useRef(null);

  // Request camera permission
  const requestPermission = async () => {
    const { status } = await Camera.requestCameraPermissionsAsync();
    setHasPermission(status === 'granted');
  };

  // Analyze image using SeeReal detection logic
  const analyzeImage = async (imageUri) => {
    setAnalyzing(true);
    
    try {
      // Simulate SeeReal analysis - replace with actual model inference
      const analysisResult = await runSeeRealAnalysis(imageUri);
      
      onAnalysisComplete({
        ...analysisResult,
        imageUri,
        timestamp: new Date().toISOString()
      });
    } catch (error) {
      Alert.alert('Analysis Error', 'Failed to analyze image');
      console.error('Analysis error:', error);
    } finally {
      setAnalyzing(false);
    }
  };

  // Take picture from camera
  const takePicture = async () => {
    if (cameraRef.current) {
      const photo = await cameraRef.current.takePictureAsync();
      analyzeImage(photo.uri);
    }
  };

  // Pick image from gallery
  const pickImage = async () => {
    const result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ImagePicker.MediaTypeOptions.Images,
      allowsEditing: true,
      quality: 1,
    });

    if (!result.cancelled) {
      analyzeImage(result.uri);
    }
  };

  // Mock SeeReal analysis (replace with actual TensorFlow.js model)
  const runSeeRealAnalysis = async (imageUri) => {
    // This would integrate with your SeeReal detection models
    return new Promise((resolve) => {
      setTimeout(() => {
        const isFake = Math.random() > 0.7; // Mock detection
        resolve({
          isFake,
          confidence: (Math.random() * 0.4 + 0.6).toFixed(2), // 0.6-1.0
          indicators: isFake ? [
            'Unnatural facial symmetry',
            'Inconsistent lighting patterns',
            'Digital artifact detection'
          ] : ['Natural facial features', 'Consistent lighting'],
          riskLevel: isFake ? 'HIGH' : 'LOW'
        });
      }, 2000);
    });
  };

  if (hasPermission === null) {
    return (
      <View style={styles.container}>
        <Text>Requesting camera permission...</Text>
        <TouchableOpacity style={styles.button} onPress={requestPermission}>
          <Text style={styles.buttonText}>Grant Camera Access</Text>
        </TouchableOpacity>
      </View>
    );
  }

  if (hasPermission === false) {
    return (
      <View style={styles.container}>
        <Text>No camera access. You can still analyze from gallery.</Text>
        <TouchableOpacity style={styles.button} onPress={pickImage}>
          <Text style={styles.buttonText}>Choose from Gallery</Text>
        </TouchableOpacity>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>🔍 SeeReal Detector</Text>
      <Text style={styles.subtitle}>Analyze images for AI manipulation</Text>
      
      <Camera style={styles.camera} type={type} ref={cameraRef}>
        <View style={styles.cameraOverlay}>
          <View style={styles.scanFrame} />
        </View>
      </Camera>

      <View style={styles.controls}>
        <TouchableOpacity 
          style={[styles.button, analyzing && styles.disabled]}
          onPress={takePicture}
          disabled={analyzing}
        >
          <Text style={styles.buttonText}>
            {analyzing ? 'Analyzing...' : '📸 Capture & Analyze'}
          </Text>
        </TouchableOpacity>

        <TouchableOpacity 
          style={[styles.button, analyzing && styles.disabled]}
          onPress={pickImage}
          disabled={analyzing}
        >
          <Text style={styles.buttonText}>
            {analyzing ? 'Analyzing...' : '🖼️ Choose from Gallery'}
          </Text>
        </TouchableOpacity>
      </View>

      {analyzing && (
        <View style={styles.analyzingContainer}>
          <Text style={styles.analyzingText}>Running SeeReal Analysis...</Text>
          <Text style={styles.analyzingSubtext}>Checking for digital artifacts and inconsistencies</Text>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginBottom: 5,
  },
  subtitle: {
    fontSize: 16,
    textAlign: 'center',
    color: '#666',
    marginBottom: 20,
  },
  camera: {
    flex: 1,
    borderRadius: 15,
    overflow: 'hidden',
    marginBottom: 20,
  },
  cameraOverlay: {
    flex: 1,
    backgroundColor: 'transparent',
    justifyContent: 'center',
    alignItems: 'center',
  },
  scanFrame: {
    width: 250,
    height: 250,
    borderWidth: 2,
    borderColor: '#4CAF50',
    borderRadius: 10,
    backgroundColor: 'transparent',
  },
  controls: {
    gap: 10,
  },
  button: {
    backgroundColor: '#2196F3',
    padding: 15,
    borderRadius: 10,
    alignItems: 'center',
  },
  disabled: {
    backgroundColor: '#cccccc',
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: '600',
  },
  analyzingContainer: {
    marginTop: 20,
    padding: 15,
    backgroundColor: '#FFF3CD',
    borderRadius: 10,
    alignItems: 'center',
  },
  analyzingText: {
    fontSize: 16,
    fontWeight: '600',
    color: '#856404',
    marginBottom: 5,
  },
  analyzingSubtext: {
    fontSize: 14,
    color: '#856404',
    textAlign: 'center',
  },
});import React, { useState } from 'react';
import { View, Text, ScrollView, StyleSheet, TouchableOpacity, Image } from 'react-native';
import SeeRealDetector from '../components/Detection/SeeRealDetector';

export default function SeeRealScreen() {
  const [analysisHistory, setAnalysisHistory] = useState([]);
  const [currentResult, setCurrentResult] = useState(null);

  const handleAnalysisComplete = (result) => {
    setCurrentResult(result);
    setAnalysisHistory(prev => [result, ...prev.slice(0, 9)]); // Keep last 10
  };

  return (
    <ScrollView style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.title}>🛡️ SeeReal Detector</Text>
        <Text style={styles.subtitle}>
          Powered by deepfake detection models + human critical thinking
        </Text>
      </View>

      {/* Live Detection Interface */}
      <SeeRealDetector onAnalysisComplete={handleAnalysisComplete} />

      {/* Current Results */}
      {currentResult && (
        <View style={[
          styles.resultCard,
          currentResult.isFake ? styles.fakeResult : styles.realResult
        ]}>
          <Text style={styles.resultTitle}>
            {currentResult.isFake ? '🚨 POTENTIALLY SYNTHETIC' : '✅ LIKELY AUTHENTIC'}
          </Text>
          <Text style={styles.confidence}>
            Confidence: {(currentResult.confidence * 100).toFixed(1)}%
          </Text>
          
          {currentResult.imageUri && (
            <Image 
              source={{ uri: currentResult.imageUri }} 
              style={styles.resultImage}
            />
          )}

          <Text style={styles.indicatorsTitle}>Detection Indicators:</Text>
          {currentResult.indicators.map((indicator, index) => (
            <Text key={index} style={styles.indicator}>
              • {indicator}
            </Text>
          ))}

          <View style={styles.riskLevel}>
            <Text style={styles.riskText}>
              Risk Level: {currentResult.riskLevel}
            </Text>
          </View>
        </View>
      )}

      {/* Analysis History */}
      {analysisHistory.length > 0 && (
        <View style={styles.historySection}>
          <Text style={styles.historyTitle}>Recent Analyses</Text>
          {analysisHistory.map((item, index) => (
            <View key={index} style={styles.historyItem}>
              <Text style={styles.historyTime}>
                {new Date(item.timestamp).toLocaleTimeString()}
              </Text>
              <Text style={[
                styles.historyResult,
                item.isFake ? styles.historyFake : styles.historyReal
              ]}>
                {item.isFake ? 'Synthetic' : 'Authentic'} 
                ({(item.confidence * 100).toFixed(0)}%)
              </Text>
            </View>
          ))}
        </View>
      )}

      {/* Educational Section */}
      <View style={styles.educationCard}>
        <Text style={styles.educationTitle}>🎓 Detection Tips</Text>
        <Text style={styles.tip}>• Look for inconsistent lighting and shadows</Text>
        <Text style={styles.tip}>• Check for unnatural facial symmetry</Text>
        <Text style={styles.tip}>• Watch for blurring around facial features</Text>
        <Text style={styles.tip}>• Analyze background consistency</Text>
        <Text style={styles.tip}>• Be wary of too-perfect skin textures</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  header: {
    padding: 20,
    alignItems: 'center',
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  subtitle: {
    fontSize: 16,
    color: '#666',
    textAlign: 'center',
  },
  resultCard: {
    margin: 20,
    padding: 15,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 6,
    elevation: 3,
  },
  fakeResult: {
    backgroundColor: '#FFE6E6',
    borderLeftWidth: 5,
    borderLeftColor: '#FF4444',
  },
  realResult: {
    backgroundColor: '#E6FFE6',
    borderLeftWidth: 5,
    borderLeftColor: '#4CAF50',
  },
  resultTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  confidence: {
    fontSize: 16,
    marginBottom: 10,
  },
  resultImage: {
    width: '100%',
    height: 200,
    borderRadius: 8,
    marginBottom: 10,
  },
  indicatorsTitle: {
    fontWeight: 'bold',
    marginBottom: 5,
  },
  indicator: {
    fontSize: 14,
    marginBottom: 2,
  },
  riskLevel: {
    marginTop: 10,
    padding: 8,
    backgroundColor: 'rgba(0,0,0,0.1)',
    borderRadius: 5,
  },
  riskText: {
    fontWeight: 'bold',
    textAlign: 'center',
  },
  historySection: {
    margin: 20,
    padding: 15,
    backgroundColor: 'white',
    borderRadius: 10,
  },
  historyTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  historyItem: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingVertical: 8,
    borderBottomWidth: 1,
    borderBottomColor: '#f0f0f0',
  },
  historyTime: {
    color: '#666',
  },
  historyResult: {
    fontWeight: '600',
  },
  historyFake: {
    color: '#FF4444',
  },
  historyReal: {
    color: '#4CAF50',
  },
  educationCard: {
    margin: 20,
    padding: 15,
    backgroundColor: '#E3F2FD',
    borderRadius: 10,
  },
  educationTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  tip: {
    fontSize: 14,
    marginBottom: 5,
  },
});import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { StatusBar } from 'expo-status-bar';

// Enhanced screens with SeeReal integration
import Onboarding from './src/screens/Onboarding';
import Dashboard from './src/screens/Dashboard';
import DrillScreen from './src/screens/DrillScreen';
import ProgressScreen from './src/screens/ProgressScreen';
import SeeRealScreen from './src/screens/SeeRealScreen'; // NEW

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <StatusBar style="auto" />
      <Stack.Navigator initialRouteName="Onboarding">
        <Stack.Screen 
          name="Onboarding" 
          component={Onboarding}
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="Dashboard" 
          component={Dashboard}
          options={{ title: 'AI Safety Suite' }}
        />
        <Stack.Screen 
          name="DrillScreen" 
          component={DrillScreen}
          options={{ title: 'Critical Thinking Training' }}
        />
        <Stack.Screen 
          name="SeeRealScreen" 
          component={SeeRealScreen}
          options={{ title: 'SeeReal Detector' }}
        />
        <Stack.Screen 
          name="ProgressScreen" 
          component={ProgressScreen}
          options={{ title: 'Your Progress' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}// Enhanced Dashboard.js
import React from 'react';
import { View, Text, TouchableOpacity, StyleSheet, ScrollView } from 'react-native';
import { LinearGradient } from 'expo-linear-gradient';

export default function Dashboard({ navigation }) {
  return (
    <ScrollView style={styles.container}>
      {/* Header */}
      <LinearGradient colors={['#667eea', '#764ba2']} style={styles.headerCard}>
        <Text style={styles.headerTitle}>🛡️ AI Safety Suite</Text>
        <Text style={styles.headerSubtitle}>SeeReal Detection + Reality Check Training</Text>
      </LinearGradient>

      {/* Quick Actions Grid */}
      <View style={styles.grid}>
        {/* SeeReal Detector Card */}
        <TouchableOpacity 
          style={[styles.card, styles.detectorCard]}
          onPress={() => navigation.navigate('SeeRealScreen')}
        >
          <Text style={styles.cardEmoji}>🔍</Text>
          <Text style={styles.cardTitle}>SeeReal Detector</Text>
          <Text style={styles.cardDescription}>Analyze images for deepfakes</Text>
          <Text style={styles.cardAction}>Scan Now →</Text>
        </TouchableOpacity>

        {/* Reality Check Training */}
        <TouchableOpacity 
          style={[styles.card, styles.trainingCard]}
          onPress={() => navigation.navigate('DrillScreen')}
        >
          <Text style={styles.cardEmoji}>🎯</Text>
          <Text style={styles.cardTitle}>Daily Training</Text>
          <Text style={styles.cardDescription}>Build detection skills</Text>
          <Text style={styles.cardAction}>Start Drill →</Text>
        </TouchableOpacity>

        {/* Progress Tracking */}
        <TouchableOpacity 
          style={[styles.card, styles.progressCard]}
          onPress={() => navigation.navigate('ProgressScreen')}
        >
          <Text style={styles.cardEmoji}>📊</Text>
          <Text style={styles.cardTitle}>Your Progress</Text>
          <Text style={styles.cardDescription}>84% accuracy</Text>
          <Text style={styles.cardAction}>View Stats →</Text>
        </TouchableOpacity>

        {/* Detection Tips */}
        <TouchableOpacity 
          style={[styles.card, styles.tipsCard]}
          onPress={() => navigation.navigate('SeeRealScreen')}
        >
          <Text style={styles.cardEmoji}>💡</Text>
          <Text style={styles.cardTitle}>Detection Guide</Text>
          <Text style={styles.cardDescription}>Learn the signs</Text>
          <Text style={styles.cardAction}>Learn More →</Text>
        </TouchableOpacity>
      </View>

      {/* Recent Activity */}
      <View style={styles.activitySection}>
        <Text style={styles.sectionTitle}>Recent Activity</Text>
        <View style={styles.activityItem}>
          <Text style={styles.activityText}>Completed deepfake detection drill</Text>
          <Text style={styles.activityTime}>2 hours ago</Text>
        </View>
        <View style={styles.activityItem}>
          <Text style={styles.activityText}>Analyzed 3 images with SeeReal</Text>
          <Text style={styles.activityTime}>Yesterday</Text>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  headerCard: {
    padding: 25,
    borderRadius: 0,
    marginBottom: 20,
  },
  headerTitle: {
    color: 'white',
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  headerSubtitle: {
    color: 'rgba(255,255,255,0.8)',
    fontSize: 16,
  },
  grid: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    padding: 10,
    justifyContent: 'space-between',
  },
  card: {
    width: '48%',
    backgroundColor: 'white',
    padding: 20,
    borderRadius: 15,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 6,
    elevation: 3,
  },
  detectorCard: {
    borderTopWidth: 4,
    borderTopColor: '#2196F3',
  },
  trainingCard: {
    borderTopWidth: 4,
    borderTopColor: '#4CAF50',
  },
  progressCard: {
    borderTopWidth: 4,
    borderTopColor: '#FF9800',
  },
  tipsCard: {
    borderTopWidth: 4,
    borderTopColor: '#9C27B0',
  },
  cardEmoji: {
    fontSize: 24,
    marginBottom: 10,
  },
  cardTitle: {
    fontSize: 16,
    fontWeight: 'bold',
    marginBottom: 5,
  },
  cardDescription: {
    fontSize: 14,
    color: '#666',
    marginBottom: 10,
  },
  cardAction: {
    fontSize: 14,
    color: '#2196F3',
    fontWeight: '600',
  },
  activitySection: {
    backgroundColor: 'white',
    margin: 20,
    padding: 20,
    borderRadius: 15,
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 15,
  },
  activityItem: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingVertical: 10,
    borderBottomWidth: 1,
    borderBottomColor: '#f0f0f0',
  },
  activityText: {
    fontSize: 14,
  },
  activityTime: {
    fontSize: 12,
    color: '#666',
  },
});reality-check-seereal/
├── SeeReal/                    # Your existing detection models
│   ├── detection_models/
│   ├── training_scripts/
│   └── dataset_utils/
├── mobile/                     # React Native app
│   ├── src/components/Detection/
│   ├── src/components/Drill/
│   └── src/screens/
├── shared/                     # Shared utilities
│   ├── model-converters/       # Convert Python models to TensorFlow.js
│   └── analysis-utils/
└── docs/
    ├── INTEGRATION.md
    └── DEPLOYMENT.md
reality-check-seereal/
├── mobile/                     # React Native App (MAIN FOCUS)
│   ├── src/
│   │   ├── components/
│   │   │   ├── Detection/     # SeeReal components
│   │   │   ├── Drill/         # Training exercises
│   │   │   └── UI/           # Reusable components
│   │   ├── screens/           # All app screens
│   │   ├── utils/             # Storage, helpers
│   │   ├── data/              # Training content
│   │   └── styles/            # Design system
│   ├── assets/               # Images, icons, videos
│   ├── app.json              # Expo config
│   ├── App.js               # Main app entry
│   └── package.json
├── backend/                  # Optional cloud backend
│   ├── models/              # ML model serving
│   ├── api/                 # REST API
│   └── database/            # User progress sync
├── docs/                    # Documentation
│   ├── LAUNCH_CHECKLIST.md
│   ├── DEPLOYMENT.md
│   └── MARKETING.md
└── scripts/                 # Build & deployment scripts{
  "name": "reality-check-seereal",
  "version": "1.0.0",
  "description": "AI Safety: Deepfake detection + critical thinking training",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web",
    "build:android": "expo build:android",
    "build:ios": "expo build:ios",
    "preview": "expo publish",
    "test": "jest"
  },
  "dependencies": {
    "expo": "~49.0.0",
    "expo-status-bar": "~1.6.0",
    "expo-camera": "~13.4.0",
    "expo-image-picker": "~14.3.0",
    "expo-av": "~13.4.0",
    "expo-sharing": "~11.3.0",
    "expo-notifications": "~0.20.1",
    "react": "18.2.0",
    "react-native": "0.72.0",
    "@react-navigation/native": "^6.1.0",
    "@react-navigation/stack": "^6.3.0",
    "@react-native-async-storage/async-storage": "1.18.0",
    "lottie-react-native": "5.1.0",
    "react-native-svg": "13.9.0",
    "axios": "^1.5.0"
  },
  "devDependencies": {
    "@babel/core": "^7.20.0",
    "jest": "^29.2.1",
    "jest-expo": "~49.0.0"
  }
}import React, { useState, useEffect } from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { StatusBar } from 'expo-status-bar';
import { View, Text } from 'react-native';

// Import all screens
import Onboarding from './src/screens/Onboarding';
import Dashboard from './src/screens/Dashboard';
import DrillScreen from './src/screens/DrillScreen';
import SeeRealScreen from './src/screens/SeeRealScreen';
import ProgressScreen from './src/screens/ProgressScreen';
import SettingsScreen from './src/screens/SettingsScreen';

// Import storage for user progress
import { Storage } from './src/utils/storage';

const Stack = createStackNavigator();

// Loading component
function LoadingScreen() {
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center', backgroundColor: '#667eea' }}>
      <Text style={{ fontSize: 24, fontWeight: 'bold', color: 'white', marginBottom: 20 }}>🛡️ Reality Check</Text>
      <Text style={{ color: 'white', fontSize: 16 }}>Loading your AI safety toolkit...</Text>
    </View>
  );
}

export default function App() {
  const [isLoading, setIsLoading] = useState(true);
  const [isFirstLaunch, setIsFirstLaunch] = useState(true);

  useEffect(() => {
    initializeApp();
  }, []);

  const initializeApp = async () => {
    try {
      // Check if user has completed onboarding
      const hasCompletedOnboarding = await Storage.getSetting('hasCompletedOnboarding');
      setIsFirstLaunch(!hasCompletedOnboarding);
    } catch (error) {
      console.error('Error initializing app:', error);
    } finally {
      setIsLoading(false);
    }
  };

  if (isLoading) {
    return <LoadingScreen />;
  }

  return (
    <NavigationContainer>
      <StatusBar style="auto" />
      <Stack.Navigator initialRouteName={isFirstLaunch ? "Onboarding" : "Dashboard"}>
        <Stack.Screen 
          name="Onboarding" 
          component={Onboarding}
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="Dashboard" 
          component={Dashboard}
          options={{ 
            title: '🛡️ AI Safety Suite',
            headerStyle: { backgroundColor: '#667eea' },
            headerTintColor: 'white'
          }}
        />
        <Stack.Screen 
          name="DrillScreen" 
          component={DrillScreen}
          options={{ title: '🎯 Training Drills' }}
        />
        <Stack.Screen 
          name="SeeRealScreen" 
          component={SeeRealScreen}
          options={{ title: '🔍 SeeReal Detector' }}
        />
        <Stack.Screen 
          name="ProgressScreen" 
          component={ProgressScreen}
          options={{ title: '📊 Your Progress' }}
        />
        <Stack.Screen 
          name="SettingsScreen" 
          component={SettingsScreen}
          options={{ title: '⚙️ Settings' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );import React, { useState } from 'react';
import { View, Text, TouchableOpacity, StyleSheet, Dimensions } from 'react-native';
import { LinearGradient } from 'expo-linear-gradient';
import { Storage } from '../utils/storage';

const { width } = Dimensions.get('window');

const onboardingSlides = [
  {
    id: 1,
    emoji: '🛡️',
    title: 'Welcome to Reality Check',
    description: 'Build your cognitive immune system against AI misinformation'
  },
  {
    id: 2,
    emoji: '🔍',
    title: 'Detect Deepfakes',
    description: 'Use SeeReal technology to analyze images and videos for AI manipulation'
  },
  {
    id: 3,
    emoji: '🎯',
    title: 'Daily Training',
    description: 'Sharpen your critical thinking skills with daily detection drills'
  },
  {
    id: 4,
    emoji: '📊',
    title: 'Track Progress',
    description: 'Monitor your improvement and earn badges as you learn'
  }
];

export default function Onboarding({ navigation }) {
  const [currentSlide, setCurrentSlide] = useState(0);

  const handleNext = async () => {
    if (currentSlide < onboardingSlides.length - 1) {
      setCurrentSlide(currentSlide + 1);
    } else {
      // Complete onboarding
      await Storage.saveSetting('hasCompletedOnboarding', true);
      navigation.replace('Dashboard');
    }
  };

  const handleSkip = async () => {
    await Storage.saveSetting('hasCompletedOnboarding', true);
    navigation.replace('Dashboard');
  };

  return (
    <View style={styles.container}>
      <LinearGradient
        colors={['#667eea', '#764ba2']}
        style={styles.gradient}
      >
        {/* Progress Dots */}
        <View style={styles.dotsContainer}>
          {onboardingSlides.map((_, index) => (
            <View
              key={index}
              style={[
                styles.dot,
                currentSlide === index && styles.activeDot
              ]}
            />
          ))}
        </View>

        {/* Content */}
        <View style={styles.content}>
          <Text style={styles.emoji}>{onboardingSlides[currentSlide].emoji}</Text>
          <Text style={styles.title}>{onboardingSlides[currentSlide].title}</Text>
          <Text style={styles.description}>{onboardingSlides[currentSlide].description}</Text>
        </View>

        {/* Buttons */}
        <View style={styles.buttonsContainer}>
          <TouchableOpacity style={styles.skipButton} onPress={handleSkip}>
            <Text style={styles.skipText}>Skip</Text>
          </TouchableOpacity>
          
          <TouchableOpacity style={styles.nextButton} onPress={handleNext}>
            <Text style={styles.nextText}>
              {currentSlide === onboardingSlides.length - 1 ? 'Get Started' : 'Next'}
            </Text>
          </TouchableOpacity>
        </View>
      </LinearGradient>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  gradient: {
    flex: 1,
    justifyContent: 'space-between',
    alignItems: 'center',
    paddingVertical: 80,
    paddingHorizontal: 30,
  },
  dotsContainer: {
    flexDirection: 'row',
    marginTop: 40,
  },
  dot: {
    width: 8,
    height: 8,
    borderRadius: 4,
    backgroundColor: 'rgba(255,255,255,0.4)',
    marginHorizontal: 4,
  },
  activeDot: {
    backgroundColor: 'white',
    width: 20,
  },
  content: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  emoji: {
    fontSize: 80,
    marginBottom: 30,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: 'white',
    textAlign: 'center',
    marginBottom: 20,
  },
  description: {
    fontSize: 18,
    color: 'rgba(255,255,255,0.9)',
    textAlign: 'center',
    lineHeight: 26,
  },
  buttonsContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    width: '100%',
  },
  skipButton: {
    padding: 15,
  },
  skipText: {
    color: 'rgba(255,255,255,0.7)',
    fontSize: 16,
  },
  nextButton: {
    backgroundColor: 'white',
    paddingHorizontal: 30,
    paddingVertical: 15,
    borderRadius: 25,
  },
  nextText: {
    color: '#667eea',
    fontSize: 16,
    fontWeight: '600',
  },
});
}import React, { useState, useEffect } from 'react';
import { View, Text, TouchableOpacity, StyleSheet, ScrollView } from 'react-native';
import DeepfakeDrill from '../components/Drill/DeepfakeDrill';
import FallacyDrill from '../components/Drill/FallacyDrill';
import SourceCheckDrill from '../components/Drill/SourceCheckDrill';
import { deepfakeDrills, fallacyDrills, sourceCheckDrills } from '../data/drills';
import { Storage } from '../utils/storage';

const DRILL_TYPES = {
  DEEPFAKE: 'deepfake',
  FALLACY: 'fallacy',
  SOURCE_CHECK: 'source_check'
};

export default function DrillScreen({ navigation }) {
  const [currentDrillType, setCurrentDrillType] = useState(DRILL_TYPES.DEEPFAKE);
  const [currentDrillIndex, setCurrentDrillIndex] = useState(0);
  const [score, setScore] = useState(0);
  const [totalAttempts, setTotalAttempts] = useState(0);
  const [drillHistory, setDrillHistory] = useState([]);
  const [isDailyComplete, setIsDailyComplete] = useState(false);

  const getCurrentDrills = () => {
    switch (currentDrillType) {
      case DRILL_TYPES.DEEPFAKE:
        return deepfakeDrills;
      case DRILL_TYPES.FALLACY:
        return fallacyDrills;
      case DRILL_TYPES.SOURCE_CHECK:
        return sourceCheckDrills;
      default:
        return deepfakeDrills;
    }
  };

  const currentDrills = getCurrentDrills();
  const currentDrill = currentDrills[currentDrillIndex];

  useEffect(() => {
    loadProgress();
  }, []);

  const loadProgress = async () => {
    const progress = await Storage.loadProgress();
    if (progress) {
      setScore(progress.score || 0);
      setTotalAttempts(progress.totalAttempts || 0);
      setDrillHistory(progress.drillHistory || []);
      setIsDailyComplete(progress.dailyComplete || false);
    }
  };

  const handleDrillComplete = async (isCorrect) => {
    const newScore = isCorrect ? score + 10 : score;
    const newTotalAttempts = totalAttempts + 1;
    const newHistory = [...drillHistory, {
      type: currentDrillType,
      drillId: currentDrill.id,
      isCorrect,
      timestamp: new Date().toISOString()
    }];

    setScore(newScore);
    setTotalAttempts(newTotalAttempts);
    setDrillHistory(newHistory);

    // Save progress
    await Storage.saveProgress({
      score: newScore,
      totalAttempts: newTotalAttempts,
      drillHistory: newHistory,
      lastDrillDate: new Date().toISOString()
    });

    // Check if should advance to next drill
    setTimeout(() => {
      if (currentDrillIndex < currentDrills.length - 1) {
        setCurrentDrillIndex(currentDrillIndex + 1);
      } else {
        // Completed all drills of this type
        handleSessionComplete();
      }
    }, 2000);
  };

  const handleSessionComplete = async () => {
    setIsDailyComplete(true);
    await Storage.saveSetting('dailyComplete', true);
    
    // Check for badge unlocks
    await checkBadgeUnlocks();
  };

  const checkBadgeUnlocks = async () => {
    const badges = await Storage.getBadges();
    const newBadges = [];

    // Check for streak badge
    const streak = await Storage.getStreak();
    if (streak >= 7 && !badges.includes('weekly_warrior')) {
      newBadges.push('weekly_warrior');
    }

    // Check for accuracy badge
    const accuracy = totalAttempts > 0 ? (score / 10) / totalAttempts : 0;
    if (accuracy >= 0.8 && totalAttempts >= 10 && !badges.includes('sharp_eye')) {
      newBadges.push('sharp_eye');
    }

    if (newBadges.length > 0) {
      await Storage.saveBadges([...badges, ...newBadges]);
    }
  };

  const resetDailyDrills = async () => {
    setCurrentDrillIndex(0);
    setIsDailyComplete(false);
    await Storage.saveSetting('dailyComplete', false);
  };

  const renderDrillComponent = () => {
    switch (currentDrillType) {
      case DRILL_TYPES.DEEPFAKE:
        return (
          <DeepfakeDrill 
            drill={currentDrill}
            onComplete={handleDrillComplete}
          />
        );
      case DRILL_TYPES.FALLACY:
        return (
          <FallacyDrill
            drill={currentDrill}
            onComplete={handleDrillComplete}
          />
        );
      case DRILL_TYPES.SOURCE_CHECK:
        return (
          <SourceCheckDrill
            drill={currentDrill}
            onComplete={handleDrillComplete}
          />
        );
      default:
        return null;
    }
  };

  if (isDailyComplete) {
    return (
      <View style={styles.container}>
        <View style={styles.completionContainer}>
          <Text style={styles.completionEmoji}>🎉</Text>
          <Text style={styles.completionTitle}>Daily Training Complete!</Text>
          <Text style={styles.completionScore}>
            Today's Score: {score} points
          </Text>
          <Text style={styles.completionAccuracy}>
            Accuracy: {totalAttempts > 0 ? Math.round((score / 10) / totalAttempts * 100) : 0}%
          </Text>
          
          <TouchableOpacity style={styles.continueButton} onPress={resetDailyDrills}>
            <Text style={styles.continueButtonText}>Practice More</Text>
          </TouchableOpacity>
          
          <TouchableOpacity style={styles.dashboardButton} onPress={() => navigation.navigate('Dashboard')}>
            <Text style={styles.dashboardButtonText}>Back to Dashboard</Text>
          </TouchableOpacity>
        </View>
      </View>
    );
  }

  return (
    <ScrollView style={styles.container}>
      {/* Drill Type Selector */}
      <View style={styles.selectorContainer}>
        <Text style={styles.selectorTitle}>Training Type:</Text>
        <View style={styles.selectorButtons}>
          <TouchableOpacity 
            style={[
              styles.selectorButton,
              currentDrillType === DRILL_TYPES.DEEPFAKE && styles.selectorButtonActive
            ]}
            onPress={() => setCurrentDrillType(DRILL_TYPES.DEEPFAKE)}
          >
            <Text style={[
              styles.selectorButtonText,
              currentDrillType === DRILL_TYPES.DEEPFAKE && styles.selectorButtonTextActive
            ]}>
              🔍 Deepfake
            </Text>
          </TouchableOpacity>
          
          <TouchableOpacity 
            style={[
              styles.selectorButton,
              currentDrillType === DRILL_TYPES.FALLACY && styles.selectorButtonActive
            ]}
            onPress={() => setCurrentDrillType(DRILL_TYPES.FALLACY)}
          >
            <Text style={[
              styles.selectorButtonText,
              currentDrillType === DRILL_TYPES.FALLACY && styles.selectorButtonTextActive
            ]}>
              🧠 Fallacies
            </Text>
          </TouchableOpacity>
          
          <TouchableOpacity 
            style={[
              styles.selectorButton,
              currentDrillType === DRILL_TYPES.SOURCE_CHECK && styles.selectorButtonActive
            ]}
            onPress={() => setCurrentDrillType(DRILL_TYPES.SOURCE_CHECK)}
          >
            <Text style={[
              styles.selectorButtonText,
              currentDrillType === DRILL_TYPES.SOURCE_CHECK && styles.selectorButtonTextActive
            ]}>
              📰 Sources
            </Text>
          </TouchableOpacity>
        </View>
      </View>

      {/* Progress Bar */}
      <View style={styles.progressContainer}>
        <Text style={styles.progressText}>
          Drill {currentDrillIndex + 1} of {currentDrills.length}
        </Text>
        <View style={styles.progressBar}>
          <View 
            style={[
              styles.progressFill,
              { width: `${((currentDrillIndex + 1) / currentDrills.length) * 100}%` }
            ]} 
          />
        </View>
      </View>

      {/* Current Drill */}
      {renderDrillComponent()}

      {/* Stats */}
      <View style={styles.statsContainer}>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>{score}</Text>
          <Text style={styles.statLabel}>Points</Text>
        </View>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>{totalAttempts}</Text>
          <Text style={styles.statLabel}>Drills</Text>
        </View>
        <View style={styles.stat}>
          <Text style={styles.statNumber}>
            {totalAttempts > 0 ? Math.round((score / 10) / totalAttempts * 100) : 0}%
          </Text>
          <Text style={styles.statLabel}>Accuracy</Text>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  selectorContainer: {
    backgroundColor: 'white',
    padding: 20,
    marginBottom: 10,
  },
  selectorTitle: {
    fontSize: 16,
    fontWeight: '600',
    marginBottom: 10,
  },
  selectorButtons: {
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  selectorButton: {
    flex: 1,
    padding: 12,
    backgroundColor: '#f0f0f0',
    borderRadius: 8,
    marginHorizontal: 5,
    alignItems: 'center',
  },
  selectorButtonActive: {
    backgroundColor: '#667eea',
  },
  selectorButtonText: {
    fontSize: 14,
    fontWeight: '500',
  },
  selectorButtonTextActive: {
    color: 'white',
  },
  progressContainer: {
    backgroundColor: 'white',
    padding: 15,
    marginBottom: 10,
  },
  progressText: {
    fontSize: 14,
    marginBottom: 5,
  },
  progressBar: {
    height: 6,
    backgroundColor: '#e0e0e0',
    borderRadius: 3,
    overflow: 'hidden',
  },
  progressFill: {
    height: '100%',
    backgroundColor: '#4CAF50',
  },
  statsContainer: {
    flexDirection: 'row',
    backgroundColor: 'white',
    padding: 20,
    marginTop: 10,
  },
  stat: {
    flex: 1,
    alignItems: 'center',
  },
  statNumber: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#333',
  },
  statLabel: {
    fontSize: 12,
    color: '#666',
    marginTop: 5,
  },
  completionContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 40,
    backgroundColor: 'white',
  },
  completionEmoji: {
    fontSize: 60,
    marginBottom: 20,
  },
  completionTitle: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 10,
    textAlign: 'center',
  },
  completionScore: {
    fontSize: 18,
    color: '#667eea',
    marginBottom: 5,
  },
  completionAccuracy: {
    fontSize: 16,
    color: '#666',
    marginBottom: 30,
  },
  continueButton: {
    backgroundColor: '#667eea',
    paddingHorizontal: 30,
    paddingVertical: 15,
    borderRadius: 25,
    marginBottom: 15,
    width: '100%',
    alignItems: 'center',
  },
  continueButtonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: '600',
  },
  dashboardButton: {
    padding: 15,
    width: '100%',
    alignItems: 'center',
  },
  dashboardButtonText: {
    color: '#667eea',
    fontSize: 16,
  },
});import AsyncStorage from '@react-native-async-storage/async-storage';

const STORAGE_KEYS = {
  USER_PROGRESS: '@reality_check_progress',
  USER_SETTINGS: '@reality_check_settings',
  BADGES: '@reality_check_badges',
  STREAK: '@reality_check_streak',
  LAST_DRILL_DATE: '@reality_check_last_drill_date'
};

export const Storage = {
  // Progress Management
  async saveProgress(progress) {
    try {
      const existing = await this.loadProgress();
      const updated = { ...existing, ...progress, updatedAt: new Date().toISOString() };
      await AsyncStorage.setItem(STORAGE_KEYS.USER_PROGRESS, JSON.stringify(updated));
      return updated;
    } catch (error) {
      console.error('Error saving progress:', error);
      return null;
    }
  },

  async loadProgress() {
    try {
      const progress = await AsyncStorage.getItem(STORAGE_KEYS.USER_PROGRESS);
      return progress ? JSON.parse(progress) : {
        score: 0,
        totalAttempts: 0,
        drillHistory: [],
        badges: [],
        createdAt: new Date().toISOString()
      };
    } catch (error) {
      console.error('Error loading progress:', error);
      return null;
    }
  },

  // Settings Management
  async saveSetting(key, value) {
    try {
      const settings = await this.getSettings();
      settings[key] = value;
      await AsyncStorage.setItem(STORAGE_KEYS.USER_SETTINGS, JSON.stringify(settings));
      return settings;
    } catch (error) {
      console.error('Error saving setting:', error);
      return null;
    }
  },

  async getSettings() {
    try {
      const settings = await AsyncStorage.getItem(STORAGE_KEYS.USER_SETTINGS);
      return settings ? JSON.parse(settings) : {};
    } catch (error) {
      console.error('Error loading settings:', error);
      return {};
    }
  },

  async getSetting(key, defaultValue = null) {
    const settings = await this.getSettings();
    return settings[key] !== undefined ? settings[key] : defaultValue;
  },

  // Streak Management
  async updateStreak() {
    try {
      const today = new Date().toDateString();
      const lastDrillDate = await AsyncStorage.getItem(STORAGE_KEYS.LAST_DRILL_DATE);
      
      let currentStreak = parseInt(await AsyncStorage.getItem(STORAGE_KEYS.STREAK) || '0');
      
      if (lastDrillDate !== today) {
        // Check if consecutive day
        const yesterday = new Date();
        yesterday.setDate(yesterday.getDate() - 1);
        
        if (lastDrillDate === yesterday.toDateString()) {
          currentStreak += 1;
        } else {
          currentStreak = 1; // Reset streak if not consecutive
        }
        
        await AsyncStorage.setItem(STORAGE_KEYS.STREAK, currentStreak.toString());
        await AsyncStorage.setItem(STORAGE_KEYS.LAST_DRILL_DATE, today);
      }
      
      return currentStreak;
    } catch (error) {
      console.error('Error updating streak:', error);
      return 0;
    }
  },

  async getStreak() {
    try {
      return parseInt(await AsyncStorage.getItem(STORAGE_KEYS.STREAK) || '0');
    } catch (error) {
      console.error('Error getting streak:', error);
      return 0;
    }
  },

  // Badge Management
  async saveBadges(badges) {
    try {
      await AsyncStorage.setItem(STORAGE_KEYS.BADGES, JSON.stringify(badges));
      return badges;
    } catch (error) {
      console.error('Error saving badges:', error);
      return [];
    }
  },

  async getBadges() {
    try {
      const badges = await AsyncStorage.getItem(STORAGE_KEYS.BADGES);
      return badges ? JSON.parse(badges) : [];
    } catch (error) {
      console.error('Error loading badges:', error);
      return [];
    }
  },

  // Data Export (for user data download)
  async exportData() {
    try {
      const progress = await this.loadProgress();
      const settings = await this.getSettings();
      const badges = await this.getBadges();
      const streak = await this.getStreak();
      
      return {
        progress,
        settings,
        badges,
        streak,
        exportDate: new Date().toISOString()
      };
    } catch (error) {
      console.error('Error exporting data:', error);
      return null;
    }
  },

  // Reset all data
  async resetAllData() {
    try {
      await AsyncStorage.multiRemove([
        STORAGE_KEYS.USER_PROGRESS,
        STORAGE_KEYS.USER_SETTINGS,
        STORAGE_KEYS.BADGES,
        STORAGE_KEYS.STREAK,
        STORAGE_KEYS.LAST_DRILL_DATE
      ]);
      return true;
    } catch (error) {
      console.error('Error resetting data:', error);
      return false;
    }
  }
};// Deepfake Detection Drills
export const deepfakeDrills = [
  {
    id: 1,
    type: 'deepfake',
    description: 'Political leader giving an emergency announcement about new regulations',
    correctAnswer: 'ai',
    feedback: 'This was AI-generated! Notice the unnatural mouth movements and inconsistent lighting on the face.',
    tellTaleSigns: 'Lip sync slightly off, robotic voice cadence, too-perfect facial symmetry',
    difficulty: 'beginner',
    points: 10,
    category: 'political'
  },
  {
    id: 2,
    type: 'deepfake',
    description: 'Celebrity endorsement for a questionable investment opportunity',
    correctAnswer: 'ai',
    feedback: 'AI-generated! Celebrities rarely make financial endorsements in this format.',
    tellTaleSigns: 'Unnatural blinking pattern, stock background, generic emotional expressions',
    difficulty: 'beginner',
    points: 10,
    category: 'financial'
  },
  {
    id: 3,
    type: 'deepfake',
    description: 'News report about a scientific breakthrough with expert interviews',
    correctAnswer: 'real',
    feedback: 'This was authentic footage from a verified news network.',
    tellTaleSigns: 'Natural camera movements, authentic background noise, verified channel branding',
    difficulty: 'beginner',
    points: 10,
    category: 'news'
  },
  {
    id: 4,
    type: 'deepfake',
    description: 'Tech CEO demonstrating a revolutionary new product',
    correctAnswer: 'ai',
    feedback: 'AI-generated! The hand movements don\'t perfectly match the product interaction.',
    tellTaleSigns: 'Hand-object occlusion issues, lighting inconsistencies, unnatural product demos',
    difficulty: 'intermediate',
    points: 15,
    category: 'tech'
  },
  {
    id: 5,
    type: 'deepfake',
    description: 'Medical professional explaining health misinformation',
    correctAnswer: 'ai',
    feedback: 'AI-generated! Medical professionals rarely make claims without proper credentials shown.',
    tellTaleSigns: 'No institutional branding, overly dramatic claims, missing credentials',
    difficulty: 'intermediate',
    points: 15,
    category: 'medical'
  }
];

// Logical Fallacy Drills
export const fallacyDrills = [
  {
    id: 1,
    type: 'fallacy',
    text: 'Either we ban all AI development immediately, or we face complete human extinction within years. There are no other options.',
    correctFallacy: 'false-dilemma',
    options: ['false-dilemma', 'slippery-slope', 'appeal-to-fear', 'straw-man'],
    feedback: 'This is a False Dilemma fallacy - presenting only two extreme options when many moderate possibilities exist.',
    explanation: 'False dilemmas ignore nuance and middle ground, forcing artificial binary choices.',
    difficulty: 'beginner',
    points: 10,
    category: 'rhetorical'
  },
  {
    id: 2,
    type: 'fallacy',
    text: 'My favorite tech influencer says this AI tool is completely safe, so it must be true - they have millions of followers!',
    correctFallacy: 'appeal-to-authority',
    options: ['appeal-to-authority', 'bandwagon', 'anecdotal', 'ad-populum'],
    feedback: 'This is an Appeal to Authority fallacy - popularity doesn\'t equal expertise or truth.',
    explanation: 'True safety requires evidence, not just influential opinions.',
    difficulty: 'beginner',
    points: 10,
    category: 'authority'
  },
  {
    id: 3,
    type: 'fallacy',
    text: 'We should ignore climate change concerns because the same people who worry about climate change also support AI regulation.',
    correctFallacy: 'guilt-by-association',
    options: ['guilt-by-association', 'red-herring', 'whataboutism', 'straw-man'],
    feedback: 'This is Guilt by Association - dismissing an issue based on unrelated positions of its supporters.',
    explanation: 'Each issue should be evaluated on its own merits, not by who supports it.',
    difficulty: 'intermediate',
    points: 15,
    category: 'association'
  }
];

// Source Verification Drills
export const sourceCheckDrills = [
  {
    id: 1,
    type: 'source_check',
    scenario: 'You see a post claiming "New AI can read your thoughts with 99% accuracy" from "AI Research Daily"',
    sources: [
      { name: 'Nature Journal', reliability: 'high', hasCoverage: false },
      { name: 'MIT Technology Review', reliability: 'high', hasCoverage: false },
      { name: 'AI Research Daily', reliability: 'low', hasCoverage: true },
      { name: 'Science Magazine', reliability: 'high', hasCoverage: false }
    ],
    correctAnswer: 'unverified',
    feedback: 'The claim comes from a low-reliability source and lacks verification from reputable scientific journals.',
    verificationSteps: [
      'Check source reputation',
      'Look for independent verification',
      'Consult expert analysis'
    ],
    difficulty: 'beginner',
    points: 10
  },
  {
    id: 2,
    type: 'source_check',
    scenario: 'A viral tweet shows "military using AI drones that make autonomous kill decisions"',
    sources: [
      { name: 'Department of Defense', reliability: 'high', hasCoverage: true, statement: 'Policy prohibits autonomous kill decisions' },
      { name: 'Reuters', reliability: 'high', hasCoverage: true, statement: 'Confirmed with military sources' },
      { name: 'Viral Twitter Account', reliability: 'low', hasCoverage: true, statement: 'Anonymous "insider" claims' },
      { name: 'UN Weapons Report', reliability: 'high', hasCoverage: false }
    ],
    correctAnswer: 'false',
    feedback: 'Official sources and reputable journalism contradict the viral claim. Autonomous kill decisions remain prohibited by policy.',
    verificationSteps: [
      'Check official statements',
      'Consult reputable journalism',
      'Verify with policy documents'
    ],
    difficulty: 'intermediate',
    points: 15
  }
];

// Badge definitions
export const badges = {
  'first_drill': {
    name: 'Getting Started',
    description: 'Complete your first detection drill',
    emoji: '🎯',
    criteria: { drillsCompleted: 1 }
  },
  'weekly_warrior': {
    name: 'Weekly Warrior',
    description: 'Complete drills for 7 consecutive days',
    emoji: '🔥',
    criteria: { streak: 7 }
  },
  'sharp_eye': {
    name: 'Sharp Eye',
    description: 'Achieve 80% accuracy on 10+ drills',
    emoji: '🔍',
    criteria: { accuracy: 0.8, minDrills: 10 }
  },
  'deepfake_detector': {
    name: 'Deepfake Detective',
    description: 'Correctly identify 20 deepfake examples',
    emoji: '🕵️',
    criteria: { deepfakesIdentified: 20 }
  },
  'critical_thinker': {
    name: 'Critical Thinker',
    description: 'Complete all fallacy detection drills',
    emoji: '🧠',
    criteria: { fallaciesCompleted: 'all' }
  }
};
