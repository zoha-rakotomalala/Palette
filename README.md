This is a new [**React Native**](https://reactnative.dev) project, bootstrapped using [`@react-native-community/cli`](https://github.com/react-native-community/cli).

# Getting Started

> **Note**: Make sure you have completed the [Set Up Your Environment](https://reactnative.dev/docs/set-up-your-environment) guide before proceeding.

## Step 1: Start Metro

First, you will need to run **Metro**, the JavaScript build tool for React Native.

To start the Metro dev server, run the following command from the root of your React Native project:

```sh
# Using npm
npm start

# OR using Yarn
yarn start
```

## Step 2: Build and run your app

With Metro running, open a new terminal window/pane from the root of your React Native project, and use one of the following commands to build and run your Android or iOS app:

### Android

```sh
# Using npm
npm run android

# OR using Yarn
yarn android
```

### iOS

For iOS, remember to install CocoaPods dependencies (this only needs to be run on first clone or after updating native deps).

The first time you create a new project, run the Ruby bundler to install CocoaPods itself:

```sh
bundle install
```

Then, and every time you update your native dependencies, run:

```sh
bundle exec pod install
```

For more information, please visit [CocoaPods Getting Started guide](https://guides.cocoapods.org/using/getting-started.html).

```sh
# Using npm
npm run ios

# OR using Yarn
yarn ios
```

If everything is set up correctly, you should see your new app running in the Android Emulator, iOS Simulator, or your connected device.

This is one way to run your app — you can also build it directly from Android Studio or Xcode.

## Step 3: Modify your app

Now that you have successfully run the app, let's make changes!

Open `App.tsx` in your text editor of choice and make some changes. When you save, your app will automatically update and reflect these changes — this is powered by [Fast Refresh](https://reactnative.dev/docs/fast-refresh).

When you want to forcefully reload, for example to reset the state of your app, you can perform a full reload:

- **Android**: Press the <kbd>R</kbd> key twice or select **"Reload"** from the **Dev Menu**, accessed via <kbd>Ctrl</kbd> + <kbd>M</kbd> (Windows/Linux) or <kbd>Cmd ⌘</kbd> + <kbd>M</kbd> (macOS).
- **iOS**: Press <kbd>R</kbd> in iOS Simulator.

## Congratulations! :tada:

You've successfully run and modified your React Native App. :partying_face:

### Now what?

- If you want to add this new React Native code to an existing application, check out the [Integration guide](https://reactnative.dev/docs/integration-with-existing-apps).
- If you're curious to learn more about React Native, check out the [docs](https://reactnative.dev/docs/getting-started).

# Troubleshooting

If you're having issues getting the above steps to work, see the [Troubleshooting](https://reactnative.dev/docs/troubleshooting) page.

# Learn More

To learn more about React Native, take a look at the following resources:

- [React Native Website](https://reactnative.dev) - learn more about React Native.
- [Getting Started](https://reactnative.dev/docs/environment-setup) - an **overview** of React Native and how setup your environment.
- [Learn the Basics](https://reactnative.dev/docs/getting-started) - a **guided tour** of the React Native **basics**.
- [Blog](https://reactnative.dev/blog) - read the latest official React Native **Blog** posts.
- [`@facebook/react-native`](https://github.com/facebook/react-native) - the Open Source; GitHub **repository** for React Native.

# :art: Building Palette from Scratch - Complete Design Plan

## :dart: **Project Overview**

**App Name**: Palette
**Purpose**: Personal art journey companion for tracking museum visits and artwork discoveries
**Platform**: Android (with potential iOS expansion)
**Development Environment**: Windows laptop

## :hammer_and_wrench: **Technology Stack Recommendation**

### **Frontend Framework Options**

#### **Option 1: React Native (Recommended)**
**Pros:**
- Single codebase for Android + iOS
- Large community and ecosystem
- Hot reload for fast development
- Native performance
- Excellent for UI-heavy apps like Palette

**Cons:**
- Steeper learning curve if new to React
- Some native features require platform-specific code

#### **Option 2: Flutter**
**Pros:**
- Single codebase for multiple platforms
- Excellent performance
- Rich UI components
- Growing rapidly

**Cons:**
- Dart language (less familiar)
- Smaller ecosystem than React Native

#### **Option 3: Native Android (Kotlin/Java)**
**Pros:**
- Full access to Android features
- Best performance
- No framework limitations

**Cons:**
- Android-only
- Longer development time
- More complex for UI-heavy apps

### **Recommended Stack: React Native + TypeScript**

```
Frontend: React Native + TypeScript
Navigation: React Navigation 6
State Management: Redux Toolkit + RTK Query
Database: SQLite (react-native-sqlite-storage)
Storage: AsyncStorage
Image Handling: react-native-image-picker + react-native-image-resizer
Offline Support: Redux Persist + Custom sync logic
UI Components: Custom components + React Native Elements
Animations: React Native Reanimated 3
Testing: Jest + React Native Testing Library
```

## :building_construction: **Project Architecture**

### **Folder Structure**
```
Palette/
├── src/
│ ├── components/ # Reusable UI components
│ │ ├── common/ # Buttons, Cards, Inputs
│ │ ├── artwork/ # Artwork-specific components
│ │ ├── museum/ # Museum-specific components
│ │ └── navigation/ # Navigation components
│ ├── screens/ # Screen components
│ │ ├── onboarding/ # Welcome flow
│ │ ├── collection/ # User's artwork collection
│ │ ├── wishlist/ # Artworks to see
│ │ ├── museums/ # Museum visits
│ │ ├── discover/ # Find new art
│ │ └── profile/ # Settings and profile
│ ├── services/ # Business logic
│ │ ├── database/ # SQLite operations
│ │ ├── api/ # External API calls
│ │ ├── sync/ # Offline sync logic
│ │ ├── photo/ # Image handling
│ │ └── storage/ # Local storage
│ ├── store/ # Redux store
│ │ ├── slices/ # Redux slices
│ │ └── middleware/ # Custom middleware
│ ├── navigation/ # Navigation configuration
│ ├── theme/ # Design system
│ │ ├── colors.ts # Color palette
│ │ ├── typography.ts # Font styles
│ │ └── spacing.ts # Layout spacing
│ ├── utils/ # Helper functions
│ ├── hooks/ # Custom React hooks
│ ├── types/ # TypeScript type definitions
│ └── constants/ # App constants
├── assets/ # Images, fonts, etc.
├── android/ # Android-specific code
├── ios/ # iOS-specific code (future)
└── __tests__/ # Test files
```

### **Core Data Models**

```typescript
// Artwork Model
interface Artwork {
  id: string;
  title: string;
  artist: Artist;
  museum: Museum;
  year?: number;
  medium?: string;
  dimensions?: string;
  description?: string;
  imageUrl?: string;
  tags: string[];
  createdAt: Date;
  updatedAt: Date;
}

// Collection Entry Model
interface CollectionEntry {
  id: string;
  artworkId: string;
  status: 'seen' | 'wishlist' | 'favorite';
  visitDate?: Date;
  museumId?: string;
  personalNotes?: string;
  rating?: number; // 1-5 stars
  photoIds: string[];
  createdAt: Date;
  updatedAt: Date;
}

// Museum Model
interface Museum {
  id: string;
  name: string;
  location: {
    address: string;
    city: string;
    country: string;
    coordinates?: {
      latitude: number;
      longitude: number;
    };
  };
  website?: string;
  description?: string;
  visitedAt?: Date[];
  createdAt: Date;
  updatedAt: Date;
}

// Artist Model
interface Artist {
  id: string;
  name: string;
  birthYear?: number;
  deathYear?: number;
  nationality?: string;
  biography?: string;
  imageUrl?: string;
  createdAt: Date;
  updatedAt: Date;
}
```

## :art: **Design System**

### **Color Palette (Pine Green & Gold Theme)**
```typescript
export const colors = {
  primary: {
    main: '#2F5233', // Pine Green
    light: '#4A7C59', // Light Pine
    dark: '#1A2E1C', // Dark Pine
  },
  secondary: {
    main: '#D4AF37', // Gold
    light: '#F4E4BC', // Light Gold
    dark: '#B8941F', // Dark Gold
  },
  neutral: {
    white: '#ffffff',
    lightGray: '#FAFAFA',
    gray: '#6B6B6B',
    darkGray: '#2C2C2C',
    black: '#000000',
  },
  semantic: {
    success: '#4A7C59',
    warning: '#D4AF37',
    error: '#C53030',
    info: '#2F5233',
  }
};
```

### **Typography Scale**
```typescript
export const typography = {
  display: {
    large: { fontSize: 36, fontWeight: '700', lineHeight: 48 },
    medium: { fontSize: 30, fontWeight: '700', lineHeight: 42 },
    small: { fontSize: 24, fontWeight: '600', lineHeight: 32 },
  },
  heading: {
    h1: { fontSize: 30, fontWeight: '700', lineHeight: 42 },
    h2: { fontSize: 24, fontWeight: '600', lineHeight: 32 },
    h3: { fontSize: 20, fontWeight: '600', lineHeight: 28 },
    h4: { fontSize: 18, fontWeight: '600', lineHeight: 26 },
  },
  body: {
    large: { fontSize: 18, fontWeight: '400', lineHeight: 28 },
    medium: { fontSize: 16, fontWeight: '400', lineHeight: 24 },
    small: { fontSize: 14, fontWeight: '400', lineHeight: 20 },
  },
  caption: {
    large: { fontSize: 14, fontWeight: '300', lineHeight: 20 },
    small: { fontSize: 12, fontWeight: '300', lineHeight: 16 },
  },
};
```

## :iphone: **Core Features to Build**

### **Phase 1: Foundation (Week 1-2)**
1. **Project Setup**
   - React Native project initialization
   - TypeScript configuration
   - Folder structure setup
   - Basic navigation

2. **Design System**
   - Color palette implementation
   - Typography system
   - Basic components (Button, Card, Input)
   - Theme provider

3. **Database Setup**
   - SQLite integration
   - Database schema design
   - Basic CRUD operations

### **Phase 2: Core Functionality (Week 3-4)**
1. **Onboarding Flow**
   - Welcome screens
   - App introduction
   - Initial setup

2. **Collection Management**
   - Add artwork to collection
   - View collection list
   - Artwork detail screen
   - Basic search functionality

3. **Museum Tracking**
   - Add museum visits
   - Museum list
   - Visit history

### **Phase 3: Enhanced Features (Week 5-6)**
1. **Photo Integration**
   - Camera integration
   - Photo gallery
   - Image optimization
   - Photo-artwork association

2. **Wishlist System**
   - Add artworks to wishlist
   - Wishlist management
   - Convert wishlist to seen

3. **Search & Discovery**
   - Advanced search
   - Filter by artist, museum, date
   - Recommendations

### **Phase 4: Polish & Advanced Features (Week 7-8)**
1. **Offline Support**
   - Data synchronization
   - Offline mode
   - Conflict resolution

2. **Settings & Customization**
   - App preferences
   - Theme selection
   - Data export/import

3. **Performance & Testing**
   - Performance optimization
   - Comprehensive testing
   - Bug fixes

## :hammer_and_wrench: **Development Tools & Setup**

### **Required Software**
1. **Node.js** (v18+) - JavaScript runtime
2. **Android Studio** - Android development environment
3. **VS Code** - Code editor with extensions:
   - React Native Tools
   - TypeScript and JavaScript Language Features
   - ES7+ React/Redux/React-Native snippets
   - Prettier - Code formatter
   - ESLint

### **Development Dependencies**
```json
{
  "devDependencies": {
    "@types/react": "^18.0.0",
    "@types/react-native": "^0.72.0",
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "eslint": "^8.0.0",
    "prettier": "^3.0.0",
    "jest": "^29.0.0",
    "@testing-library/react-native": "^12.0.0"
  }
}
```

### **Production Dependencies**
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-native": "^0.72.0",
    "@react-navigation/native": "^6.1.0",
    "@react-navigation/bottom-tabs": "^6.5.0",
    "@react-navigation/stack": "^6.3.0",
    "@reduxjs/toolkit": "^1.9.0",
    "react-redux": "^8.1.0",
    "redux-persist": "^6.0.0",
    "react-native-sqlite-storage": "^6.0.0",
    "@react-native-async-storage/async-storage": "^1.19.0",
    "react-native-image-picker": "^5.6.0",
    "react-native-image-resizer": "^1.4.5",
    "react-native-reanimated": "^3.5.0",
    "react-native-gesture-handler": "^2.12.0",
    "react-native-safe-area-context": "^4.7.0",
    "react-native-screens": "^3.25.0"
  }
}
```

## :clipboard: **Development Phases Timeline**

### **Week 1-2: Foundation**
- [ ] Set up React Native project
- [ ] Configure TypeScript
- [ ] Implement basic navigation
- [ ] Create design system components
- [ ] Set up SQLite database

### **Week 3-4: Core Features**
- [ ] Build onboarding flow
- [ ] Implement collection management
- [ ] Create artwork detail screens
- [ ] Add museum tracking
- [ ] Basic search functionality

### **Week 5-6: Enhanced Features**
- [ ] Integrate camera and photo handling
- [ ] Build wishlist system
- [ ] Advanced search and filters
- [ ] Recommendation engine
- [ ] Data synchronization

### **Week 7-8: Polish & Testing**
- [ ] Offline support
- [ ] Settings and preferences
- [ ] Performance optimization
- [ ] Comprehensive testing
- [ ] Bug fixes and polish

## :rocket: **Getting Started Steps**

### **1. Environment Setup**
```bash
# Install Node.js from nodejs.org
# Install Android Studio
# Install React Native CLI
npm install -g react-native-cli

# Create new project
npx react-native init Palette --template react-native-template-typescript
cd Palette
```

### **2. Install Core Dependencies**
```bash
npm install @react-navigation/native @react-navigation/bottom-tabs @react-navigation/stack
npm install @reduxjs/toolkit react-redux redux-persist
npm install react-native-sqlite-storage @react-native-async-storage/async-storage
npm install react-native-image-picker react-native-image-resizer
npm install react-native-reanimated react-native-gesture-handler
npm install react-native-safe-area-context react-native-screens
```

### **3. Configure Android**
```bash
# Link native dependencies (if needed)
npx react-native link

# Run on Android
npx react-native run-android
```

## :dart: **Success Metrics**

### **Technical Goals**
- [ ] App launches in <3 seconds
- [ ] Smooth 60fps animations
- [ ] Works offline seamlessly
- [ ] <1% crash rate
- [ ] Supports Android 7+ (API 24+)

### **Feature Goals**
- [ ] Add artwork to collection in <30 seconds
- [ ] Search results in <2 seconds
- [ ] Photo capture and association in <1 minute
- [ ] Sync data in background without user intervention

### **User Experience Goals**
- [ ] Intuitive navigation (no tutorial needed)
- [ ] Beautiful, museum-quality design
- [ ] Accessible (screen reader compatible)
- [ ] Responsive on various screen sizes

## :bulb: **Pro Tips for Development**

1. **Start Simple**: Begin with basic functionality, add complexity gradually
2. **Use TypeScript**: Catch errors early and improve code quality
3. **Test on Real Device**: Use your Android phone for testing
4. **Version Control**: Use Git from day one
5. **Incremental Development**: Build feature by feature
6. **Performance First**: Optimize as you build, not after
7. **User Feedback**: Test with friends/family early and often

## :books: **Learning Resources**

- **React Native Docs**: [reactnative.dev](https://reactnative.dev/)
- **TypeScript Handbook**: [typescriptlang.org](https://www.typescriptlang.org/)
- **Redux Toolkit**: [redux-toolkit.js.org](https://redux-toolkit.js.org/)
- **React Navigation**: [reactnavigation.org](https://reactnavigation.org/)

---

**This plan gives you a complete roadmap to build Palette from scratch in ~8 weeks, with a professional, production-ready result!** :art::iphone:

Would you like me to elaborate on any specific part of this plan?
