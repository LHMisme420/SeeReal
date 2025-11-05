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
