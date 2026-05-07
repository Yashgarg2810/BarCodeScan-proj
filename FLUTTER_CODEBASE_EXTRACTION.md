# SmartLabelScan - React to Flutter Codebase Extraction

## 📱 Application Overview

**App Name:** SmartLabelScan  
**Purpose:** Mobile health app for tracking allergies and dietary preferences through product scanning  
**Architecture:** Single Page Application with component-based architecture  
**Navigation:** Bottom tab navigation with screen transitions  

---

## 🏗️ App Structure & Navigation Flow

### Main App Component (`App.tsx`)
```typescript
// Navigation state management
type Screen = 'splash' | 'guest-scan' | 'personal-info' | 'health-goals' | 
              'dietary-preferences' | 'allergies' | 'completion' | 'home' | 
              'camera-scan' | 'product-detail' | 'scan-history' | 'profile' | 
              'product-comparison';

// Main navigation flow
SplashScreen → GuestScanScreen → OnboardingFlow → HomeScreen
```

### Navigation Patterns
1. **Linear Onboarding Flow**: PersonalInfo → HealthGoals → DietaryPreferences → Allergies → Completion
2. **Tab Navigation**: Home, Scan, History, Profile (authenticated users)
3. **Modal/Overlay**: ProductDetail, ProductComparison screens
4. **Stack Navigation**: Back button support throughout flows

---

## 🎨 Design System Specifications

### Color Palette
```css
/* Primary Colors */
--primary-green: #4CAF50;
--primary-green-light: #81C784;
--primary-green-dark: #388E3C;

/* UI Colors */
--background: #FAFAFA;
--card-background: #FFFFFF;
--border: #E0E0E0;
--text-primary: #212121;
--text-secondary: #757575;
--text-muted: #9E9E9E;

/* Status Colors */
--success: #4CAF50;
--warning: #FF9800;
--error: #F44336;
--info: #2196F3;

/* Nutri-Score Colors */
--nutri-a: #4CAF50;
--nutri-b: #8BC34A;
--nutri-c: #FF9800;
--nutri-d: #FF5722;
--nutri-e: #F44336;
```

### Typography System
```css
/* Font Families */
--font-primary: 'Poppins', sans-serif; /* Headers */
--font-secondary: 'Inter', sans-serif;  /* Body text */

/* Font Scales */
--text-3xl: 1.875rem;  /* 30px */
--text-2xl: 1.5rem;    /* 24px */
--text-xl: 1.25rem;    /* 20px */
--text-lg: 1.125rem;   /* 18px */
--text-base: 1rem;     /* 16px */
--text-sm: 0.875rem;   /* 14px */
--text-xs: 0.75rem;    /* 12px */

/* Line Heights */
--leading-tight: 1.25;
--leading-snug: 1.375;
--leading-normal: 1.5;
--leading-relaxed: 1.625;
```

### Spacing System
```css
/* Spacing Scale (in rem) */
--spacing-1: 0.25rem;   /* 4px */
--spacing-2: 0.5rem;    /* 8px */
--spacing-3: 0.75rem;   /* 12px */
--spacing-4: 1rem;      /* 16px */
--spacing-5: 1.25rem;   /* 20px */
--spacing-6: 1.5rem;    /* 24px */
--spacing-8: 2rem;      /* 32px */
--spacing-12: 3rem;     /* 48px */
--spacing-16: 4rem;     /* 64px */
```

### Border Radius
```css
--radius-sm: 0.5rem;    /* 8px */
--radius-md: 0.75rem;   /* 12px */
--radius-lg: 1rem;      /* 16px */
--radius-xl: 1.5rem;    /* 24px */
--radius-full: 9999px;  /* Circular */
```

---

## 📱 Screen Components Specifications

### 1. SplashScreen
```typescript
interface SplashScreenProps {
  onLoadingComplete: () => void;
}

// Features:
- Animated logo with pulse effect
- Progress indicator (0-100%)
- Loading text rotation: ["Initializing...", "Loading scan engine...", "Preparing health database...", "Almost ready..."]
- 3-second total duration
- Gradient background with pattern overlay
```

### 2. GuestScanScreen
```typescript
interface GuestScanScreenProps {
  onNavigate: (screen: string) => void;
}

// Layout Sections:
1. Header: "Hello, Guest! 👋" with guest badge
2. Action buttons: Scan Product (primary) | My Profile (secondary)
3. Scan usage card: "0/10 scans remaining"
4. Sign up encouragement card with benefits
5. Benefits showcase section
6. Health tips carousel
7. Bottom CTA card
8. Bottom navigation (4 tabs)

// Key Features:
- Scan counter tracking (guest limit: 10 scans)
- Benefits highlighting for registration
- Health tips rotation
- Responsive card layouts
```

### 3. OnboardingFlow Components

#### PersonalInfoOnboarding
```typescript
interface PersonalInfoData {
  name: string;
  gender: 'Male' | 'Female' | 'Other';
  dateOfBirth: Date;
  age: number;
}

// Form Elements:
- Text input: Full name (validation: min 2 chars)
- Gender selector: 3 options in horizontal pills
- Date picker: DOB with age auto-calculation
- Continue button: Validates all fields
```

#### HealthGoalsOnboarding
```typescript
interface HealthGoalsData {
  selectedGoals: string[];
}

const healthGoalOptions = [
  "Weight Management",
  "Heart Health", 
  "Digestive Health",
  "Energy & Vitality",
  "Muscle Building",
  "Better Sleep",
  "Immune Support",
  "Mental Clarity"
];

// Features:
- Multi-select chip interface
- Visual icons for each goal
- Minimum 1 selection required
- Animated selection states
```

#### DietaryPreferencesOnboarding
```typescript
interface DietaryPreferencesData {
  selectedPreferences: string[];
}

const dietaryOptions = [
  "Vegetarian",
  "Vegan", 
  "Keto",
  "Paleo",
  "Mediterranean",
  "Low Carb",
  "Gluten-Free",
  "Dairy-Free",
  "Low Sodium",
  "High Protein"
];

// Features:
- Grid layout with preference cards
- Icons and descriptions for each option
- Multiple selection allowed
- Skip option available
```

#### AllergiesOnboarding
```typescript
interface AllergiesData {
  selectedAllergies: string[];
  severityLevels: Record<string, 'mild' | 'moderate' | 'severe'>;
}

const commonAllergies = [
  { name: "Nuts", icon: "🥜", category: "Tree Nuts" },
  { name: "Dairy", icon: "🥛", category: "Dairy" },
  { name: "Gluten", icon: "🌾", category: "Grains" },
  { name: "Eggs", icon: "🥚", category: "Animal Products" },
  { name: "Shellfish", icon: "🦐", category: "Seafood" },
  { name: "Soy", icon: "🫘", category: "Legumes" },
  { name: "Fish", icon: "🐟", category: "Seafood" },
  { name: "Sesame", icon: "🌰", category: "Seeds" }
];

// Features:
- Allergy selection with severity levels
- Search functionality for additional allergies
- Visual indicators for severity
- Warning explanations for each level
```

### 4. CompletionCelebration
```typescript
interface CompletionCelebrationProps {
  userProfile: UserProfile;
  onContinue: () => void;
}

// Features:
- Animated checkmark icon
- Personalized congratulations message
- Profile summary display
- Lottie celebration animation
- Continue to home button
```

### 5. HomeScreen (Authenticated)
```typescript
interface HomeScreenProps {
  userProfile: UserProfile;
  onNavigate: (screen: string) => void;
}

// Layout Sections:
1. Header: Greeting with notification badge
2. Search bar: Product/ingredient search
3. Quick actions: 2x2 grid (Scan, Search, History, Profile)
4. Health metrics: 3 metric cards with trends
5. Recent scans: Horizontal scrolling list
6. Personalized tips: Vertical card stack
7. Bottom navigation: 4 tabs

// Data Elements:
- Recent scans (limit: 4 visible)
- Health metrics with trend indicators
- Personalized tips based on preferences
- Notification count display
```

### 6. CameraScanScreen
```typescript
interface CameraScanScreenProps {
  onScanComplete: (result: ScanResult) => void;
  onCancel: () => void;
}

// Features:
- Camera viewfinder with overlay
- Barcode/QR detection frame
- Manual photo capture button
- Flash toggle
- Gallery import option
- Scanning animation overlay
- Auto-focus functionality
```

### 7. ProductDetailScreen
```typescript
interface ProductDetailScreenProps {
  productId: string;
  scanResult?: ScanResult;
  onBack: () => void;
  onCompare: () => void;
}

// Content Sections:
1. Product header: Image, name, brand, Nutri-Score
2. Compatibility indicators: Allergies, dietary preferences
3. Nutrition facts: Expandable table
4. Ingredients analysis: Detailed breakdown
5. Health insights: Personalized recommendations
6. Action buttons: Save, Share, Compare
7. Alternative suggestions: Related products

// Key Features:
- Allergy warnings with severity levels
- Dietary compatibility checks
- Nutritional traffic light system
- Ingredient concern highlighting
- Personalized health scoring
```

### 8. ScanHistoryScreen
```typescript
interface ScanHistoryScreenProps {
  scans: ScanResult[];
  onScanSelect: (scanId: string) => void;
}

// Features:
- Chronological scan list
- Search and filter options
- Nutri-Score visual indicators
- Swipe-to-delete functionality
- Empty state for new users
- Infinite scroll/pagination
- Export functionality
```

### 9. ProfileScreen
```typescript
interface ProfileScreenProps {
  userProfile: UserProfile;
  onProfileUpdate: (updates: Partial<UserProfile>) => void;
  onLogout: () => void;
}

// Sections:
1. Profile header: Avatar, name, stats
2. Health profile: Goals, preferences, allergies
3. Scan statistics: Charts and metrics
4. App preferences: Notifications, privacy
5. Account management: Export data, delete account
6. Support: Help, feedback, about

// Features:
- Editable profile fields
- Statistics visualization
- Privacy controls
- Data export options
```

### 10. ProductComparisonScreen
```typescript
interface ProductComparisonScreenProps {
  products: ProductDetail[];
  onRemoveProduct: (productId: string) => void;
  onAddProduct: () => void;
}

// Features:
- Side-by-side product comparison
- Nutrition facts table comparison
- Ingredient analysis comparison
- Health score comparison
- Winner highlighting
- Add/remove products (max 3)
```

---

## 🧩 Reusable Component Library

### Button Components

#### PrimaryButton
```typescript
interface PrimaryButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
  disabled?: boolean;
  loading?: boolean;
  icon?: React.ReactNode;
  variant?: 'default' | 'destructive';
  size?: 'sm' | 'md' | 'lg';
  fullWidth?: boolean;
}

// Styling:
- Green background (#4CAF50)
- White text
- 12px border radius
- 16px vertical padding
- Loading spinner overlay
- Disabled state styling
```

#### SecondaryButton
```typescript
interface SecondaryButtonProps extends PrimaryButtonProps {
  variant?: 'outline' | 'ghost';
}

// Styling:
- Transparent background
- Green border and text
- Same sizing as PrimaryButton
- Hover state effects
```

### Card Components

#### RecentScanCard
```typescript
interface RecentScanCardProps {
  id: string;
  productName: string;
  brandName?: string;
  imageUrl: string;
  nutriScore: 'A' | 'B' | 'C' | 'D' | 'E';
  scannedAt: string;
  onClick: () => void;
}

// Layout:
- 144px fixed width
- Product image with Nutri-Score badge
- Product name (2 lines max)
- Brand name (1 line, secondary text)
- Scan timestamp
- Rounded corners, subtle shadow
```

#### HealthMetricCard
```typescript
interface HealthMetricCardProps {
  label: string;
  value: string;
  trend?: string;
  icon: string;
  trendDirection?: 'up' | 'down' | 'stable';
}

// Features:
- Metric value with large typography
- Trend indicator with color coding
- Icon representation
- Compact card layout
```

#### PersonalizedTip
```typescript
interface PersonalizedTipProps {
  id: number;
  title: string;
  description: string;
  icon: string;
  category: string;
}

// Layout:
- Horizontal card with icon
- Title and description text
- Category badge
- Expandable content option
```

### Form Components

#### SelectableChip
```typescript
interface SelectableChipProps {
  label: string;
  selected: boolean;
  onToggle: () => void;
  icon?: React.ReactNode;
  disabled?: boolean;
}

// States:
- Default: Light background, border
- Selected: Green background, white text
- Disabled: Muted colors
- Hover: Subtle scale animation
```

### UI Components

#### NutriScoreBadge
```typescript
interface NutriScoreBadgeProps {
  score: 'A' | 'B' | 'C' | 'D' | 'E';
  size?: 'sm' | 'md' | 'lg';
}

// Color mapping:
- A: Green (#4CAF50)
- B: Light green (#8BC34A)
- C: Orange (#FF9800)
- D: Orange-red (#FF5722)
- E: Red (#F44336)
```

#### ProgressRing
```typescript
interface ProgressRingProps {
  progress: number; // 0-100
  size: number;
  strokeWidth: number;
  color?: string;
  showPercentage?: boolean;
}

// Features:
- Animated progress fill
- Customizable colors
- Smooth transitions
- Optional percentage display
```

#### BottomNavBar
```typescript
interface BottomNavBarProps {
  activeTab: 'home' | 'scan' | 'history' | 'profile';
  onTabChange: (tab: string) => void;
  className?: string;
}

// Features:
- Fixed bottom positioning
- Active state indicators
- Smooth tab transitions
- Badge support for notifications
- Responsive width (max 375px)
```

---

## 📊 Data Models & Types

### Core Data Models

#### UserProfile
```typescript
interface UserProfile {
  id: string;
  name: string;
  email?: string;
  gender: 'Male' | 'Female' | 'Other';
  dateOfBirth: Date;
  age: number;
  createdAt: Date;
  updatedAt: Date;
  
  // Health data
  healthGoals: string[];
  dietaryPreferences: string[];
  allergies: AllergyInfo[];
  
  // App preferences
  notifications: NotificationSettings;
  privacy: PrivacySettings;
  
  // Statistics
  totalScans: number;
  weeklyScans: number;
  healthScore: number;
}

interface AllergyInfo {
  name: string;
  severity: 'mild' | 'moderate' | 'severe';
  category: string;
}

interface NotificationSettings {
  scanReminders: boolean;
  healthTips: boolean;
  productAlerts: boolean;
  weeklyReports: boolean;
}

interface PrivacySettings {
  dataSharing: boolean;
  analyticsTracking: boolean;
  marketingEmails: boolean;
}
```

#### ScanResult
```typescript
interface ScanResult {
  id: string;
  userId: string;
  productId: string;
  scannedAt: Date;
  scanMethod: 'barcode' | 'image' | 'manual';
  location?: GeolocationCoordinates;
  
  // Product data
  product: ProductDetail;
  
  // Analysis results
  compatibility: CompatibilityAnalysis;
  healthInsights: HealthInsight[];
  alternatives: ProductSuggestion[];
}

interface ProductDetail {
  id: string;
  name: string;
  brand: string;
  barcode?: string;
  imageUrl: string;
  category: string;
  
  // Nutrition data
  nutriScore: 'A' | 'B' | 'C' | 'D' | 'E';
  nutritionFacts: NutritionFacts;
  ingredients: Ingredient[];
  
  // Metadata
  servingSize: string;
  packageSize: string;
  countryOfOrigin?: string;
  certifications: string[];
}

interface NutritionFacts {
  calories: number;
  totalFat: number;
  saturatedFat: number;
  transFat: number;
  cholesterol: number;
  sodium: number;
  totalCarbs: number;
  dietaryFiber: number;
  totalSugars: number;
  addedSugars: number;
  protein: number;
  
  // Percentages based on daily values
  percentDailyValues: Record<string, number>;
}

interface Ingredient {
  name: string;
  percentage?: number;
  allergenInfo?: string[];
  additiveType?: 'preservative' | 'colorant' | 'flavor' | 'sweetener';
  concerns?: string[];
}

interface CompatibilityAnalysis {
  overallScore: number; // 0-10
  allergyWarnings: AllergyWarning[];
  dietaryCompatibility: DietaryCompatibility[];
  healthScore: number;
  concerns: string[];
  benefits: string[];
}

interface AllergyWarning {
  allergen: string;
  severity: 'mild' | 'moderate' | 'severe';
  confidence: number;
  source: 'ingredient' | 'manufacturing' | 'cross-contamination';
}

interface DietaryCompatibility {
  diet: string;
  compatible: boolean;
  reason?: string;
  alternatives?: string[];
}

interface HealthInsight {
  type: 'positive' | 'negative' | 'neutral';
  title: string;
  description: string;
  impact: 'low' | 'medium' | 'high';
  category: 'nutrition' | 'ingredients' | 'processing';
}

interface ProductSuggestion {
  product: ProductDetail;
  reason: string;
  score: number;
  priceComparison?: 'lower' | 'similar' | 'higher';
}
```

#### HealthMetric
```typescript
interface HealthMetric {
  id: string;
  userId: string;
  date: Date;
  
  // Metrics
  weeklyScans: number;
  healthScore: number;
  goalsProgress: GoalProgress[];
  nutrientIntake: NutrientSummary;
  
  // Trends
  scanTrend: 'up' | 'down' | 'stable';
  healthTrend: 'up' | 'down' | 'stable';
}

interface GoalProgress {
  goal: string;
  current: number;
  target: number;
  unit: string;
  achieved: boolean;
}

interface NutrientSummary {
  averageNutriScore: number;
  sodiumAverage: number;
  fiberAverage: number;
  sugarAverage: number;
  proteinAverage: number;
}
```

---

## 🔄 State Management Patterns

### App State Structure
```typescript
interface AppState {
  // Navigation
  currentScreen: Screen;
  navigationHistory: Screen[];
  
  // User data
  isAuthenticated: boolean;
  isGuestMode: boolean;
  userProfile: UserProfile | null;
  
  // Scan data
  recentScans: ScanResult[];
  scanHistory: ScanResult[];
  currentScan: ScanResult | null;
  
  // UI state
  isLoading: boolean;
  errors: ErrorState[];
  notifications: Notification[];
  
  // Cache
  productCache: Record<string, ProductDetail>;
  userPreferences: UserPreferences;
}

interface ErrorState {
  id: string;
  type: 'network' | 'validation' | 'scan' | 'system';
  message: string;
  timestamp: Date;
  dismissed: boolean;
}

interface Notification {
  id: string;
  type: 'info' | 'success' | 'warning' | 'error';
  title: string;
  message: string;
  timestamp: Date;
  read: boolean;
  actions?: NotificationAction[];
}

interface NotificationAction {
  label: string;
  action: () => void;
  primary?: boolean;
}
```

### State Management Actions
```typescript
// User actions
LOGIN_SUCCESS
LOGOUT
UPDATE_PROFILE
SET_GUEST_MODE

// Navigation actions
NAVIGATE_TO
GO_BACK
RESET_NAVIGATION

// Scan actions
START_SCAN
SCAN_SUCCESS
SCAN_ERROR
ADD_TO_HISTORY
CLEAR_CURRENT_SCAN

// Data actions
LOAD_RECENT_SCANS
LOAD_SCAN_HISTORY
UPDATE_HEALTH_METRICS
CACHE_PRODUCT

// UI actions
SET_LOADING
ADD_ERROR
DISMISS_ERROR
ADD_NOTIFICATION
MARK_NOTIFICATION_READ
```

---

## 🛠️ API Integration Patterns

### API Service Structure
```typescript
class ApiService {
  private baseUrl = 'https://api.smartlabelscan.com';
  private apiKey = process.env.REACT_APP_API_KEY;
  
  // Authentication
  async login(email: string, password: string): Promise<AuthResponse>;
  async register(userData: UserRegistration): Promise<AuthResponse>;
  async refreshToken(): Promise<TokenResponse>;
  
  // User management
  async getUserProfile(userId: string): Promise<UserProfile>;
  async updateUserProfile(userId: string, updates: Partial<UserProfile>): Promise<UserProfile>;
  
  // Scanning
  async scanBarcode(barcode: string): Promise<ProductDetail>;
  async analyzeImage(imageData: string): Promise<ScanResult>;
  async getProductDetails(productId: string): Promise<ProductDetail>;
  
  // History
  async getScanHistory(userId: string, limit?: number): Promise<ScanResult[]>;
  async deleteScan(scanId: string): Promise<void>;
  
  // Recommendations
  async getProductAlternatives(productId: string, userProfile: UserProfile): Promise<ProductSuggestion[]>;
  async getPersonalizedTips(userId: string): Promise<PersonalizedTip[]>;
  
  // Analytics
  async getHealthMetrics(userId: string, dateRange: DateRange): Promise<HealthMetric[]>;
  async trackScanEvent(userId: string, scanData: ScanEvent): Promise<void>;
}
```

### Error Handling Patterns
```typescript
interface ApiError {
  code: string;
  message: string;
  details?: any;
  timestamp: Date;
}

// Common error codes
const ErrorCodes = {
  NETWORK_ERROR: 'NETWORK_ERROR',
  PRODUCT_NOT_FOUND: 'PRODUCT_NOT_FOUND',
  SCAN_FAILED: 'SCAN_FAILED',
  RATE_LIMITED: 'RATE_LIMITED',
  UNAUTHORIZED: 'UNAUTHORIZED',
  VALIDATION_ERROR: 'VALIDATION_ERROR'
} as const;
```

---

## 📱 Platform-Specific Features

### Camera Integration
```typescript
interface CameraService {
  requestPermissions(): Promise<boolean>;
  startCamera(): Promise<void>;
  stopCamera(): Promise<void>;
  capturePhoto(): Promise<string>; // base64 image
  toggleFlash(): Promise<void>;
  switchCamera(): Promise<void>; // front/back
}

interface BarcodeScanner {
  startScanning(): Promise<void>;
  stopScanning(): Promise<void>;
  onBarcodeDetected: (barcode: string) => void;
  supportedFormats: BarcodeFormat[];
}
```

### Storage Patterns
```typescript
interface StorageService {
  // User data
  setUserProfile(profile: UserProfile): Promise<void>;
  getUserProfile(): Promise<UserProfile | null>;
  clearUserData(): Promise<void>;
  
  // Scan history
  addScanResult(scan: ScanResult): Promise<void>;
  getScanHistory(limit?: number): Promise<ScanResult[]>;
  deleteScan(scanId: string): Promise<void>;
  
  // App preferences
  setPreference(key: string, value: any): Promise<void>;
  getPreference(key: string): Promise<any>;
  
  // Cache management
  setCachedProduct(productId: string, product: ProductDetail): Promise<void>;
  getCachedProduct(productId: string): Promise<ProductDetail | null>;
  clearCache(): Promise<void>;
}
```

### Offline Support
```typescript
interface OfflineManager {
  isOnline: boolean;
  syncPendingScans(): Promise<void>;
  getCachedData(key: string): Promise<any>;
  queueForSync(action: SyncAction): Promise<void>;
  onConnectivityChange: (isOnline: boolean) => void;
}

interface SyncAction {
  type: 'scan' | 'profile_update' | 'preference_change';
  data: any;
  timestamp: Date;
  retryCount: number;
}
```

---

## 🎬 Animation & Transition Specifications

### Page Transitions
```css
/* Slide up transition */
.slide-up-enter {
  transform: translateY(100%);
  opacity: 0;
}
.slide-up-enter-active {
  transform: translateY(0);
  opacity: 1;
  transition: all 300ms ease-out;
}

/* Fade transition */
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  opacity: 1;
  transition: opacity 200ms ease-in;
}

/* Scale transition for modals */
.scale-enter {
  transform: scale(0.9);
  opacity: 0;
}
.scale-enter-active {
  transform: scale(1);
  opacity: 1;
  transition: all 250ms cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Component Animations
```typescript
// Button press animation
const buttonTapAnimation = {
  scale: 0.95,
  transition: { duration: 0.1 }
};

// Loading spinner
const spinnerAnimation = {
  rotate: 360,
  transition: { 
    duration: 1,
    repeat: Infinity,
    ease: "linear"
  }
};

// Progress ring animation
const progressRingAnimation = {
  pathLength: [0, 1],
  transition: { 
    duration: 1.5,
    ease: "easeInOut"
  }
};

// Card hover animation
const cardHoverAnimation = {
  y: -4,
  boxShadow: "0 8px 24px rgba(0,0,0,0.12)",
  transition: { duration: 0.2 }
};
```

---

## 🧪 Testing Patterns

### Component Testing
```typescript
// Example test structure for components
describe('PrimaryButton', () => {
  it('renders with correct text');
  it('handles click events');
  it('shows loading state');
  it('is disabled when disabled prop is true');
  it('applies correct styling variants');
});

describe('ScanHistoryScreen', () => {
  it('displays empty state when no scans');
  it('renders scan list correctly');
  it('handles scan selection');
  it('supports search functionality');
  it('implements infinite scroll');
});
```

### Integration Testing
```typescript
// User flow testing
describe('Onboarding Flow', () => {
  it('completes full onboarding process');
  it('validates form inputs correctly');
  it('navigates between steps properly');
  it('saves user data on completion');
});

describe('Scanning Flow', () => {
  it('opens camera successfully');
  it('processes barcode scan');
  it('displays product details');
  it('saves scan to history');
});
```

---

## 📦 Dependencies & Libraries

### Core Dependencies
```json
{
  "react": "^18.2.0",
  "react-dom": "^18.2.0",
  "typescript": "^5.0.0",
  "tailwindcss": "^3.3.0"
}
```

### UI & Animation Libraries
```json
{
  "lucide-react": "^0.259.0",
  "framer-motion": "^10.16.0",
  "react-spring": "^9.7.0",
  "lottie-react": "^2.4.0"
}
```

### Utility Libraries
```json
{
  "date-fns": "^2.30.0",
  "clsx": "^2.0.0",
  "react-hook-form": "^7.45.0",
  "zod": "^3.22.0"
}
```

### Camera & Scanning
```json
{
  "react-camera-pro": "^1.4.0",
  "quagga": "^0.12.1",
  "@zxing/library": "^0.20.0"
}
```

---

## 🚀 Build & Deployment Configuration

### Environment Variables
```env
REACT_APP_API_URL=https://api.smartlabelscan.com
REACT_APP_API_KEY=your_api_key_here
REACT_APP_ENVIRONMENT=production
REACT_APP_ANALYTICS_ID=your_analytics_id
REACT_APP_SENTRY_DSN=your_sentry_dsn
```

### Build Configuration
```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives",
    "type-check": "tsc --noEmit"
  }
}
```

---

## 📋 Flutter Migration Checklist

### Priority 1 - Core Screens
- [ ] SplashScreen with loading animation
- [ ] GuestScanScreen with all sections
- [ ] Onboarding flow (4 screens)
- [ ] HomeScreen for authenticated users
- [ ] Basic navigation between screens

### Priority 2 - Scanning Features
- [ ] Camera integration
- [ ] Barcode scanning capability
- [ ] Product detail display
- [ ] Scan history management

### Priority 3 - User Management
- [ ] Profile creation and editing
- [ ] Preferences management
- [ ] Data persistence
- [ ] Authentication flow

### Priority 4 - Advanced Features
- [ ] Product comparison
- [ ] Health insights
- [ ] Personalized recommendations
- [ ] Analytics and metrics

### Priority 5 - Polish & Optimization
- [ ] Animations and transitions
- [ ] Offline support
- [ ] Performance optimization
- [ ] Accessibility features

---

This extraction document provides a comprehensive blueprint for recreating the SmartLabelScan React application in Flutter, with detailed specifications for every component, feature, and interaction pattern.