# SmartLabelScan - Flutter UI Flow Specification

## 📱 Application Overview

**App Name:** SmartLabelScan  
**Platform:** Flutter (iOS & Android)  
**Purpose:** Mobile health app for tracking allergies and dietary preferences through product scanning  
**Target Users:** Health-conscious consumers, people with allergies/dietary restrictions  

### Key Features
- Product barcode/image scanning
- Allergy and dietary preference management
- Personalized health recommendations
- Nutritional analysis and insights
- Guest mode with limited functionality
- User onboarding and profile creation

---

## 🎨 Design System

### Color Palette
```dart
// Primary Colors
const Color primaryGreen = Color(0xFF4CAF50);
const Color primaryGreenLight = Color(0xFF81C784);
const Color primaryGreenDark = Color(0xFF388E3C);

// Secondary Colors
const Color accentBlue = Color(0xFF2196F3);
const Color accentOrange = Color(0xFFF57C00);
const Color accentPurple = Color(0xFF9C27B0);

// Neutral Colors
const Color backgroundLight = Color(0xFFFAFAFA);
const Color backgroundDark = Color(0xFF121212);
const Color cardBackground = Color(0xFFFFFFFF);
const Color borderLight = Color(0xFFE0E0E0);
const Color textPrimary = Color(0xFF212121);
const Color textSecondary = Color(0xFF757575);
const Color textMuted = Color(0xFF9E9E9E);

// Status Colors
const Color successGreen = Color(0xFF4CAF50);
const Color warningOrange = Color(0xFFFF9800);
const Color errorRed = Color(0xFFF44336);
const Color infoBlue = Color(0xFF2196F3);
```

### Typography
```dart
// Font Family: Poppins (Primary), Inter (Secondary)
const TextStyle headingLarge = TextStyle(
  fontFamily: 'Poppins',
  fontSize: 24,
  fontWeight: FontWeight.bold,
  letterSpacing: -0.5,
);

const TextStyle headingMedium = TextStyle(
  fontFamily: 'Poppins',
  fontSize: 20,
  fontWeight: FontWeight.w600,
  letterSpacing: -0.3,
);

const TextStyle headingSmall = TextStyle(
  fontFamily: 'Poppins',
  fontSize: 18,
  fontWeight: FontWeight.w600,
);

const TextStyle bodyLarge = TextStyle(
  fontFamily: 'Inter',
  fontSize: 16,
  fontWeight: FontWeight.normal,
  height: 1.5,
);

const TextStyle bodyMedium = TextStyle(
  fontFamily: 'Inter',
  fontSize: 14,
  fontWeight: FontWeight.normal,
  height: 1.4,
);

const TextStyle bodySmall = TextStyle(
  fontFamily: 'Inter',
  fontSize: 12,
  fontWeight: FontWeight.normal,
  height: 1.3,
);

const TextStyle labelMedium = TextStyle(
  fontFamily: 'Inter',
  fontSize: 14,
  fontWeight: FontWeight.w500,
  letterSpacing: 0.1,
);
```

### Spacing System
```dart
// Standard spacing values (in logical pixels)
const double spacing4 = 4.0;
const double spacing8 = 8.0;
const double spacing12 = 12.0;
const double spacing16 = 16.0;
const double spacing20 = 20.0;
const double spacing24 = 24.0;
const double spacing32 = 32.0;
const double spacing48 = 48.0;
const double spacing64 = 64.0;
```

### Border Radius
```dart
const BorderRadius radiusSmall = BorderRadius.all(Radius.circular(8.0));
const BorderRadius radiusMedium = BorderRadius.all(Radius.circular(12.0));
const BorderRadius radiusLarge = BorderRadius.all(Radius.circular(16.0));
const BorderRadius radiusXLarge = BorderRadius.all(Radius.circular(24.0));
```

---

## 🗺️ Application Flow

### Main Navigation Flow
```
SplashScreen → GuestScanScreen ↔ OnboardingFlow → HomeScreen
                    ↓                    ↓
                CameraScan            AuthenticatedApp
                    ↓                    ↓
                ProductDetail        [Profile, History, etc.]
```

### Screen Hierarchy
1. **SplashScreen** (Entry Point)
2. **GuestScanScreen** (Guest Mode)
3. **OnboardingFlow** (4 screens)
   - PersonalInfoOnboarding
   - HealthGoalsOnboarding
   - DietaryPreferencesOnboarding
   - AllergiesOnboarding
4. **CompletionCelebration**
5. **HomeScreen** (Authenticated)
6. **Additional Screens**
   - CameraScanScreen
   - ProductDetailScreen
   - ScanHistoryScreen
   - ProfileScreen

---

## 📱 Screen Specifications

### 1. SplashScreen
**File Reference:** `components/SplashScreen.tsx`

#### Layout Structure
```
AppBar: None
Body: 
  - Centered Column
    - App Logo (Animated)
    - App Title: "SmartLabelScan"
    - Subtitle: "Your health companion for smarter choices"
    - Progress Indicator
    - Loading Text (Dynamic)
    - Version Info (Bottom)
```

#### Components Needed
```dart
class SplashScreen extends StatefulWidget {
  final VoidCallback onLoadingComplete;
  
  @override
  _SplashScreenState createState() => _SplashScreenState();
}

class _SplashScreenState extends State<SplashScreen> 
    with TickerProviderStateMixin {
  
  late AnimationController _pulseController;
  late AnimationController _progressController;
  
  double _progress = 0.0;
  String _loadingText = 'Initializing...';
  
  final List<String> _loadingMessages = [
    'Initializing...',
    'Loading scan engine...',
    'Preparing health database...',
    'Almost ready...'
  ];
}
```

#### Visual Elements
- **Logo**: 96x96 dp circular container with green gradient
- **Pulse Animation**: Two concentric circles with ping animation
- **Progress Bar**: Linear progress indicator (green theme)
- **Loading Messages**: Animated text changes every 800ms
- **Version Text**: Bottom positioned, muted color

#### Animations
1. **Logo Pulse**: Scale animation with opacity changes
2. **Progress Bar**: Linear progression from 0% to 100%
3. **Text Fade**: Crossfade between loading messages

---

### 2. GuestScanScreen
**File Reference:** `components/GuestScanScreen.tsx`

#### Layout Structure
```
AppBar: Custom header with guest badge
Body: ScrollView
  - Header Section
  - Action Buttons (Side by side)
  - Scan Usage Card
  - Sign Up Encouragement Card
  - Benefits Section
  - Tips Section
  - CTA Card
BottomNavigationBar: 4 tabs
```

#### Header Section
```dart
class GuestHeader extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(24),
      decoration: BoxDecoration(
        gradient: LinearGradient(
          begin: Alignment.topCenter,
          end: Alignment.bottomCenter,
          colors: [Color(0xFFF1F8E9), Colors.transparent],
        ),
      ),
      child: Row(
        children: [
          // App Icon
          Container(
            width: 48,
            height: 48,
            decoration: BoxDecoration(
              color: Color(0xFFC8E6C9),
              borderRadius: BorderRadius.circular(24),
            ),
            child: Icon(Icons.scanner, color: primaryGreen),
          ),
          SizedBox(width: 12),
          // Text Section
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text('Hello, Guest! 👋', style: headingMedium),
                Text('Ready to identify what you intake?', 
                     style: bodyMedium.copyWith(color: textSecondary)),
              ],
            ),
          ),
          // Guest Badge
          Container(
            padding: EdgeInsets.symmetric(horizontal: 12, vertical: 6),
            decoration: BoxDecoration(
              color: Color(0xFFC8E6C9),
              borderRadius: BorderRadius.circular(12),
              border: Border.all(color: Color(0xFF81C784)),
            ),
            child: Text('Guest Mode', style: labelMedium),
          ),
        ],
      ),
    );
  }
}
```

#### Action Buttons Section
```dart
class ActionButtonsSection extends StatelessWidget {
  final VoidCallback onScanProduct;
  final VoidCallback onCreateProfile;

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.all(24),
      padding: EdgeInsets.all(16),
      decoration: BoxDecoration(
        color: cardBackground,
        borderRadius: radiusMedium,
        border: Border.all(color: borderLight),
      ),
      child: Row(
        children: [
          // Scan Product Button
          Expanded(
            child: GestureDetector(
              onTap: onScanProduct,
              child: Container(
                padding: EdgeInsets.all(16),
                decoration: BoxDecoration(
                  color: primaryGreen,
                  borderRadius: radiusMedium,
                ),
                child: Column(
                  children: [
                    Container(
                      width: 48,
                      height: 48,
                      decoration: BoxDecoration(
                        color: Colors.white.withOpacity(0.2),
                        borderRadius: radiusMedium,
                      ),
                      child: Icon(Icons.qr_code_scanner, 
                                  color: Colors.white, size: 24),
                    ),
                    SizedBox(height: 8),
                    Text('Scan Product', 
                         style: labelMedium.copyWith(color: Colors.white)),
                    Text('Scan barcode or take photo',
                         style: bodySmall.copyWith(
                           color: Colors.white.withOpacity(0.9))),
                  ],
                ),
              ),
            ),
          ),
          SizedBox(width: 16),
          // Create Profile Button
          Expanded(
            child: GestureDetector(
              onTap: onCreateProfile,
              child: Container(
                padding: EdgeInsets.all(16),
                decoration: BoxDecoration(
                  color: backgroundLight,
                  borderRadius: radiusMedium,
                  border: Border.all(color: borderLight),
                ),
                child: Column(
                  children: [
                    Container(
                      width: 48,
                      height: 48,
                      decoration: BoxDecoration(
                        color: Color(0xFFC8E6C9),
                        borderRadius: radiusMedium,
                      ),
                      child: Icon(Icons.person, 
                                  color: primaryGreen, size: 24),
                    ),
                    SizedBox(height: 8),
                    Text('My Profile', style: labelMedium),
                    Text('Manage preferences', 
                         style: bodySmall.copyWith(color: textSecondary)),
                  ],
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

#### Scan Usage Card
```dart
class ScanUsageCard extends StatelessWidget {
  final int currentScans;
  final int totalScans;

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.symmetric(horizontal: 24, vertical: 12),
      padding: EdgeInsets.all(16),
      decoration: BoxDecoration(
        gradient: LinearGradient(
          colors: [Color(0xFFE3F2FD), Color(0xFFE8EAF6)],
        ),
        borderRadius: radiusMedium,
        border: Border.all(color: Color(0xFF90CAF9)),
      ),
      child: Column(
        children: [
          // Header
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Row(
                children: [
                  Icon(Icons.qr_code_scanner, color: accentBlue),
                  SizedBox(width: 8),
                  Text('Scan Usage', style: labelMedium),
                ],
              ),
              Container(
                padding: EdgeInsets.symmetric(horizontal: 8, vertical: 4),
                decoration: BoxDecoration(
                  color: Color(0xFFBBDEFB),
                  borderRadius: BorderRadius.circular(8),
                  border: Border.all(color: Color(0xFF90CAF9)),
                ),
                child: Text('Free Trial', style: bodySmall),
              ),
            ],
          ),
          SizedBox(height: 12),
          // Usage Stats
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Text('Scans: $currentScans', 
                   style: bodyMedium.copyWith(color: textSecondary)),
              Text('Total Scans Available: $totalScans',
                   style: headingSmall.copyWith(color: accentBlue)),
            ],
          ),
          SizedBox(height: 12),
          // Progress Bar
          LinearProgressIndicator(
            value: currentScans / totalScans,
            backgroundColor: Color(0xFFBBDEFB),
            valueColor: AlwaysStoppedAnimation<Color>(accentBlue),
          ),
        ],
      ),
    );
  }
}
```

#### Sign Up Encouragement Card
```dart
class SignUpEncouragementCard extends StatelessWidget {
  final VoidCallback onSignUp;

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.symmetric(horizontal: 24, vertical: 12),
      padding: EdgeInsets.all(16),
      decoration: BoxDecoration(
        gradient: LinearGradient(
          colors: [Color(0xFFFFF3E0), Color(0xFFFFF8E1)],
        ),
        borderRadius: radiusMedium,
        border: Border.all(color: Color(0xFFFFCC02)),
      ),
      child: Column(
        children: [
          // Header with Icon
          Row(
            children: [
              Container(
                width: 48,
                height: 48,
                decoration: BoxDecoration(
                  gradient: LinearGradient(
                    colors: [accentOrange, Color(0xFFFFC107)],
                  ),
                  borderRadius: BorderRadius.circular(24),
                ),
                child: Icon(Icons.card_giftcard, 
                           color: Colors.white, size: 24),
              ),
              SizedBox(width: 12),
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text('Want to add more free scans?', 
                         style: labelMedium),
                    Text('Get unlimited scans and personalized insights',
                         style: bodySmall.copyWith(color: textSecondary)),
                  ],
                ),
              ),
            ],
          ),
          SizedBox(height: 16),
          // Sign Up Button
          SizedBox(
            width: double.infinity,
            child: ElevatedButton.icon(
              onPressed: onSignUp,
              icon: Icon(Icons.add, color: Colors.white),
              label: Text('Sign Up With Us', 
                          style: labelMedium.copyWith(color: Colors.white)),
              style: ElevatedButton.styleFrom(
                backgroundColor: accentOrange,
                padding: EdgeInsets.symmetric(vertical: 12),
                shape: RoundedRectangleBorder(
                  borderRadius: radiusMedium,
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

---

### 3. OnboardingFlow

#### PersonalInfoOnboarding
**File Reference:** `components/PersonalInfoOnboarding.tsx`

##### Form Fields
```dart
class PersonalInfoForm extends StatefulWidget {
  final Function(PersonalInfo) onComplete;

  @override
  _PersonalInfoFormState createState() => _PersonalInfoFormState();
}

class _PersonalInfoFormState extends State<PersonalInfoForm> {
  final _formKey = GlobalKey<FormState>();
  final _nameController = TextEditingController();
  
  String _selectedGender = '';
  DateTime? _selectedDate;
  
  final List<String> _genderOptions = ['Male', 'Female', 'Other'];
}
```

##### Gender Selection Widget
```dart
class GenderSelector extends StatelessWidget {
  final String selectedGender;
  final Function(String) onGenderSelected;
  final List<String> options;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text('Gender', style: labelMedium),
        SizedBox(height: 8),
        Row(
          children: options.map((gender) {
            final isSelected = selectedGender == gender;
            return Expanded(
              child: GestureDetector(
                onTap: () => onGenderSelected(gender),
                child: Container(
                  margin: EdgeInsets.only(right: 8),
                  padding: EdgeInsets.symmetric(vertical: 16),
                  decoration: BoxDecoration(
                    color: isSelected ? primaryGreen : backgroundLight,
                    borderRadius: radiusMedium,
                    border: Border.all(
                      color: isSelected ? primaryGreen : borderLight,
                    ),
                  ),
                  child: Center(
                    child: Text(
                      gender,
                      style: labelMedium.copyWith(
                        color: isSelected ? Colors.white : textPrimary,
                      ),
                    ),
                  ),
                ),
              ),
            );
          }).toList(),
        ),
      ],
    );
  }
}
```

#### HealthGoalsOnboarding
**File Reference:** `components/HealthGoalsOnboarding.tsx`

##### SelectableChip Widget
```dart
class SelectableChip extends StatelessWidget {
  final String label;
  final bool isSelected;
  final VoidCallback onTap;
  final IconData? icon;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onTap,
      child: AnimatedContainer(
        duration: Duration(milliseconds: 200),
        padding: EdgeInsets.symmetric(horizontal: 16, vertical: 12),
        decoration: BoxDecoration(
          color: isSelected ? primaryGreen : backgroundLight,
          borderRadius: radiusMedium,
          border: Border.all(
            color: isSelected ? primaryGreen : borderLight,
            width: isSelected ? 2 : 1,
          ),
        ),
        child: Row(
          mainAxisSize: MainAxisSize.min,
          children: [
            if (icon != null) ...[
              Icon(
                icon,
                size: 16,
                color: isSelected ? Colors.white : textSecondary,
              ),
              SizedBox(width: 8),
            ],
            Text(
              label,
              style: bodyMedium.copyWith(
                color: isSelected ? Colors.white : textPrimary,
                fontWeight: isSelected ? FontWeight.w600 : FontWeight.normal,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### AllergiesOnboarding
**File Reference:** `components/AllergiesOnboarding.tsx`

##### Allergies List
```dart
final List<Map<String, dynamic>> allergiesList = [
  {'name': 'Nuts', 'icon': '🥜', 'severity': 'high'},
  {'name': 'Dairy', 'icon': '🥛', 'severity': 'medium'},
  {'name': 'Gluten', 'icon': '🌾', 'severity': 'medium'},
  {'name': 'Eggs', 'icon': '🥚', 'severity': 'medium'},
  {'name': 'Shellfish', 'icon': '🦐', 'severity': 'high'},
  {'name': 'Soy', 'icon': '🫘', 'severity': 'low'},
  {'name': 'Fish', 'icon': '🐟', 'severity': 'medium'},
  {'name': 'Sesame', 'icon': '🌰', 'severity': 'medium'},
];
```

---

### 4. HomeScreen (Authenticated)
**File Reference:** `components/HomeScreen.tsx`

#### Layout Structure
```dart
class HomeScreen extends StatefulWidget {
  final UserProfile userProfile;
  final Function(String) onNavigate;

  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  String _searchQuery = '';
  final List<RecentScan> _recentScans = [];
  final List<HealthMetric> _healthMetrics = [];
  final List<PersonalizedTip> _tips = [];
}
```

#### Header Section
```dart
class HomeHeader extends StatelessWidget {
  final String userName;
  final int notificationCount;

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.fromLTRB(24, 48, 24, 24),
      decoration: BoxDecoration(
        gradient: LinearGradient(
          begin: Alignment.topCenter,
          end: Alignment.bottomCenter,
          colors: [Color(0xFFF1F8E9), Colors.transparent],
        ),
      ),
      child: Row(
        children: [
          // App Icon and Greeting
          Row(
            children: [
              Container(
                width: 48,
                height: 48,
                decoration: BoxDecoration(
                  color: Color(0xFFC8E6C9),
                  borderRadius: BorderRadius.circular(24),
                ),
                child: Icon(Icons.scanner, color: primaryGreen),
              ),
              SizedBox(width: 12),
              Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text('Hello, $userName! 👋', style: headingMedium),
                  Text('Ready to make healthy choices?',
                       style: bodyMedium.copyWith(color: textSecondary)),
                ],
              ),
            ],
          ),
          Spacer(),
          // Notification Button
          Stack(
            children: [
              IconButton(
                onPressed: () {},
                icon: Icon(Icons.notifications_outlined, 
                          color: textSecondary),
              ),
              if (notificationCount > 0)
                Positioned(
                  right: 8,
                  top: 8,
                  child: Container(
                    width: 16,
                    height: 16,
                    decoration: BoxDecoration(
                      color: primaryGreen,
                      borderRadius: BorderRadius.circular(8),
                    ),
                    child: Center(
                      child: Text(
                        '$notificationCount',
                        style: TextStyle(
                          color: Colors.white,
                          fontSize: 10,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ),
                  ),
                ),
            ],
          ),
        ],
      ),
    );
  }
}
```

#### Recent Scans Horizontal List
```dart
class RecentScansSection extends StatelessWidget {
  final List<RecentScan> scans;
  final VoidCallback onViewAll;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Section Header
        Padding(
          padding: EdgeInsets.symmetric(horizontal: 24),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Text('Recent Scans', style: headingSmall),
              TextButton(
                onPressed: onViewAll,
                child: Text('View All', 
                           style: bodyMedium.copyWith(color: primaryGreen)),
              ),
            ],
          ),
        ),
        SizedBox(height: 16),
        // Horizontal Scroll List
        SizedBox(
          height: 200,
          child: ListView.builder(
            scrollDirection: Axis.horizontal,
            padding: EdgeInsets.symmetric(horizontal: 24),
            itemCount: scans.length,
            itemBuilder: (context, index) {
              return Padding(
                padding: EdgeInsets.only(right: 12),
                child: RecentScanCard(scan: scans[index]),
              );
            },
          ),
        ),
      ],
    );
  }
}
```

#### RecentScanCard Widget
```dart
class RecentScanCard extends StatelessWidget {
  final RecentScan scan;

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 144,
      decoration: BoxDecoration(
        color: cardBackground,
        borderRadius: radiusMedium,
        border: Border.all(color: borderLight),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.05),
            blurRadius: 8,
            offset: Offset(0, 2),
          ),
        ],
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          // Product Image with Nutri-Score Badge
          Stack(
            children: [
              ClipRRect(
                borderRadius: BorderRadius.vertical(top: Radius.circular(12)),
                child: Image.network(
                  scan.imageUrl,
                  width: double.infinity,
                  height: 96,
                  fit: BoxFit.cover,
                ),
              ),
              Positioned(
                top: 8,
                right: 8,
                child: Container(
                  padding: EdgeInsets.symmetric(horizontal: 6, vertical: 2),
                  decoration: BoxDecoration(
                    color: _getNutriScoreColor(scan.nutriScore),
                    borderRadius: BorderRadius.circular(12),
                  ),
                  child: Text(
                    scan.nutriScore,
                    style: TextStyle(
                      color: Colors.white,
                      fontSize: 12,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
              ),
            ],
          ),
          // Product Info
          Padding(
            padding: EdgeInsets.all(12),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  scan.productName,
                  style: labelMedium,
                  maxLines: 2,
                  overflow: TextOverflow.ellipsis,
                ),
                if (scan.brandName != null) ...[
                  SizedBox(height: 4),
                  Text(
                    scan.brandName!,
                    style: bodySmall.copyWith(color: textSecondary),
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                  ),
                ],
                SizedBox(height: 8),
                Text(
                  scan.scannedAt,
                  style: bodySmall.copyWith(color: textMuted),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Color _getNutriScoreColor(String score) {
    switch (score) {
      case 'A': return successGreen;
      case 'B': return Color(0xFF8BC34A);
      case 'C': return warningOrange;
      case 'D': return Color(0xFFFF5722);
      case 'E': return errorRed;
      default: return Color(0xFF9E9E9E);
    }
  }
}
```

---

## 🧩 Reusable Components

### PrimaryButton
```dart
class PrimaryButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;
  final IconData? icon;
  final bool isLoading;
  final bool isEnabled;

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: double.infinity,
      child: ElevatedButton(
        onPressed: isEnabled && !isLoading ? onPressed : null,
        style: ElevatedButton.styleFrom(
          backgroundColor: primaryGreen,
          disabledBackgroundColor: Color(0xFFE0E0E0),
          padding: EdgeInsets.symmetric(vertical: 16),
          shape: RoundedRectangleBorder(
            borderRadius: radiusMedium,
          ),
          elevation: 0,
        ),
        child: isLoading
            ? SizedBox(
                height: 20,
                width: 20,
                child: CircularProgressIndicator(
                  strokeWidth: 2,
                  valueColor: AlwaysStoppedAnimation<Color>(Colors.white),
                ),
              )
            : Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  if (icon != null) ...[
                    Icon(icon, color: Colors.white, size: 20),
                    SizedBox(width: 8),
                  ],
                  Text(
                    text,
                    style: labelMedium.copyWith(color: Colors.white),
                  ),
                ],
              ),
      ),
    );
  }
}
```

### SecondaryButton
```dart
class SecondaryButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;
  final IconData? icon;
  final bool isEnabled;

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: double.infinity,
      child: OutlinedButton(
        onPressed: isEnabled ? onPressed : null,
        style: OutlinedButton.styleFrom(
          side: BorderSide(color: primaryGreen),
          padding: EdgeInsets.symmetric(vertical: 16),
          shape: RoundedRectangleBorder(
            borderRadius: radiusMedium,
          ),
        ),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            if (icon != null) ...[
              Icon(icon, color: primaryGreen, size: 20),
              SizedBox(width: 8),
            ],
            Text(
              text,
              style: labelMedium.copyWith(color: primaryGreen),
            ),
          ],
        ),
      ),
    );
  }
}
```

### BottomNavBar
```dart
class BottomNavBar extends StatelessWidget {
  final int currentIndex;
  final Function(int) onTap;

  final List<BottomNavItem> _items = [
    BottomNavItem(icon: Icons.home, label: 'Home'),
    BottomNavItem(icon: Icons.qr_code_scanner, label: 'Scan'),
    BottomNavItem(icon: Icons.history, label: 'History'),
    BottomNavItem(icon: Icons.person, label: 'Profile'),
  ];

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
        color: cardBackground,
        border: Border(top: BorderSide(color: borderLight, width: 0.5)),
      ),
      child: SafeArea(
        child: Padding(
          padding: EdgeInsets.symmetric(vertical: 8),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceAround,
            children: _items.asMap().entries.map((entry) {
              final index = entry.key;
              final item = entry.value;
              final isActive = currentIndex == index;
              
              return GestureDetector(
                onTap: () => onTap(index),
                child: Container(
                  padding: EdgeInsets.symmetric(vertical: 8, horizontal: 16),
                  decoration: BoxDecoration(
                    color: isActive ? primaryGreen.withOpacity(0.1) : null,
                    borderRadius: radiusMedium,
                  ),
                  child: Column(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      Icon(
                        item.icon,
                        color: isActive ? primaryGreen : textSecondary,
                        size: 24,
                      ),
                      SizedBox(height: 4),
                      Text(
                        item.label,
                        style: bodySmall.copyWith(
                          color: isActive ? primaryGreen : textSecondary,
                          fontWeight: isActive ? FontWeight.w600 : FontWeight.normal,
                        ),
                      ),
                    ],
                  ),
                ),
              );
            }).toList(),
          ),
        ),
      ),
    );
  }
}

class BottomNavItem {
  final IconData icon;
  final String label;
  
  BottomNavItem({required this.icon, required this.label});
}
```

---

## 🔄 State Management

### App State Structure
```dart
// Use Provider or Riverpod for state management

class AppState {
  bool isGuestMode;
  UserProfile? userProfile;
  List<RecentScan> recentScans;
  List<HealthMetric> healthMetrics;
  AppScreen currentScreen;
  
  AppState({
    this.isGuestMode = true,
    this.userProfile,
    this.recentScans = const [],
    this.healthMetrics = const [],
    this.currentScreen = AppScreen.splash,
  });
}

enum AppScreen {
  splash,
  guestScan,
  personalInfo,
  healthGoals,
  dietaryPreferences,
  allergies,
  completion,
  home,
  cameraScan,
  productDetail,
  scanHistory,
  profile,
}
```

### User Profile Model
```dart
class UserProfile {
  final String name;
  final String gender;
  final DateTime dateOfBirth;
  final int age;
  final List<String> healthGoals;
  final List<String> dietaryPreferences;
  final List<String> allergies;
  
  UserProfile({
    required this.name,
    required this.gender,
    required this.dateOfBirth,
    required this.age,
    required this.healthGoals,
    required this.dietaryPreferences,
    required this.allergies,
  });
  
  factory UserProfile.fromJson(Map<String, dynamic> json) {
    return UserProfile(
      name: json['name'],
      gender: json['gender'],
      dateOfBirth: DateTime.parse(json['dateOfBirth']),
      age: json['age'],
      healthGoals: List<String>.from(json['healthGoals']),
      dietaryPreferences: List<String>.from(json['dietaryPreferences']),
      allergies: List<String>.from(json['allergies']),
    );
  }
  
  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'gender': gender,
      'dateOfBirth': dateOfBirth.toIso8601String(),
      'age': age,
      'healthGoals': healthGoals,
      'dietaryPreferences': dietaryPreferences,
      'allergies': allergies,
    };
  }
}
```

### Recent Scan Model
```dart
class RecentScan {
  final String id;
  final String productName;
  final String? brandName;
  final String imageUrl;
  final String nutriScore;
  final String scannedAt;
  
  RecentScan({
    required this.id,
    required this.productName,
    this.brandName,
    required this.imageUrl,
    required this.nutriScore,
    required this.scannedAt,
  });
  
  factory RecentScan.fromJson(Map<String, dynamic> json) {
    return RecentScan(
      id: json['id'],
      productName: json['productName'],
      brandName: json['brandName'],
      imageUrl: json['imageUrl'],
      nutriScore: json['nutriScore'],
      scannedAt: json['scannedAt'],
    );
  }
}
```

---

## 📐 Layout Guidelines

### Screen Padding
- **Horizontal Padding**: 24dp on all screens
- **Vertical Spacing**: 16dp between sections
- **Card Padding**: 16dp internal padding
- **Button Padding**: 16dp vertical, full width

### Responsive Design
```dart
class ResponsiveLayout {
  static double getHorizontalPadding(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    if (screenWidth > 600) {
      return 48.0; // Tablet
    }
    return 24.0; // Mobile
  }
  
  static double getMaxWidth(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    return screenWidth > 600 ? 400.0 : screenWidth;
  }
}
```

### Safe Area Handling
```dart
class SafeAreaWrapper extends StatelessWidget {
  final Widget child;
  final bool top;
  final bool bottom;
  
  @override
  Widget build(BuildContext context) {
    return SafeArea(
      top: top,
      bottom: bottom,
      child: child,
    );
  }
}
```

---

## 🎬 Animations

### Page Transitions
```dart
class SlideUpPageRoute<T> extends PageRouteBuilder<T> {
  final Widget child;
  
  SlideUpPageRoute({required this.child})
      : super(
          pageBuilder: (context, animation, secondaryAnimation) => child,
          transitionsBuilder: (context, animation, secondaryAnimation, child) {
            const begin = Offset(0.0, 1.0);
            const end = Offset.zero;
            const curve = Curves.easeInOut;
            
            var tween = Tween(begin: begin, end: end)
                .chain(CurveTween(curve: curve));
            
            return SlideTransition(
              position: animation.drive(tween),
              child: child,
            );
          },
          transitionDuration: Duration(milliseconds: 300),
        );
}
```

### Button Tap Animation
```dart
class TapAnimationWrapper extends StatefulWidget {
  final Widget child;
  final VoidCallback onTap;
  
  @override
  _TapAnimationWrapperState createState() => _TapAnimationWrapperState();
}

class _TapAnimationWrapperState extends State<TapAnimationWrapper>
    with SingleTickerProviderStateMixin {
  
  late AnimationController _controller;
  late Animation<double> _scaleAnimation;
  
  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(milliseconds: 100),
      vsync: this,
    );
    _scaleAnimation = Tween<double>(begin: 1.0, end: 0.95)
        .animate(CurvedAnimation(parent: _controller, curve: Curves.easeInOut));
  }
  
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTapDown: (_) => _controller.forward(),
      onTapUp: (_) {
        _controller.reverse();
        widget.onTap();
      },
      onTapCancel: () => _controller.reverse(),
      child: AnimatedBuilder(
        animation: _scaleAnimation,
        builder: (context, child) {
          return Transform.scale(
            scale: _scaleAnimation.value,
            child: widget.child,
          );
        },
      ),
    );
  }
}
```

---

## 📱 Platform-Specific Considerations

### iOS
- Use `CupertinoPageRoute` for navigation
- Implement pull-to-refresh with `CupertinoSliverRefreshControl`
- Use iOS-style date picker for date selection
- Handle safe area properly with notch devices

### Android
- Use Material Design components consistently
- Implement Material You theming (Android 12+)
- Handle back button navigation properly
- Use Material date picker

### Common
- Implement proper keyboard handling
- Handle different screen densities
- Support both light and dark themes
- Implement proper accessibility features

---

## 🔧 Technical Requirements

### Dependencies
```yaml
dependencies:
  flutter: ^3.16.0
  provider: ^6.1.1  # or riverpod
  shared_preferences: ^2.2.2
  http: ^1.1.0
  image_picker: ^1.0.4
  qr_code_scanner: ^1.0.1
  cached_network_image: ^3.3.0
  intl: ^0.18.1
  lottie: ^2.7.0
  
dev_dependencies:
  flutter_test: ^3.16.0
  flutter_lints: ^3.0.1
```

### File Structure
```
lib/
├── main.dart
├── app.dart
├── models/
│   ├── user_profile.dart
│   ├── recent_scan.dart
│   ├── health_metric.dart
│   └── personalized_tip.dart
├── screens/
│   ├── splash_screen.dart
│   ├── guest_scan_screen.dart
│   ├── onboarding/
│   │   ├── personal_info_screen.dart
│   │   ├── health_goals_screen.dart
│   │   ├── dietary_preferences_screen.dart
│   │   └── allergies_screen.dart
│   ├── home_screen.dart
│   ├── camera_scan_screen.dart
│   └── profile_screen.dart
├── widgets/
│   ├── buttons/
│   │   ├── primary_button.dart
│   │   └── secondary_button.dart
│   ├── cards/
│   │   ├── recent_scan_card.dart
│   │   └── health_metric_card.dart
│   ├── navigation/
│   │   └── bottom_nav_bar.dart
│   └── common/
│       ├── selectable_chip.dart
│       └── tap_animation_wrapper.dart
├── services/
│   ├── api_service.dart
│   ├── storage_service.dart
│   └── scan_service.dart
├── providers/
│   ├── app_state_provider.dart
│   └── user_provider.dart
├── constants/
│   ├── colors.dart
│   ├── text_styles.dart
│   └── dimensions.dart
└── utils/
    ├── date_formatter.dart
    └── validators.dart
```

### Storage
- Use `SharedPreferences` for simple data storage
- Implement secure storage for sensitive data
- Cache network images appropriately
- Store user preferences locally

### API Integration
```dart
class ApiService {
  static const String baseUrl = 'https://api.smartlabelscan.com';
  
  Future<ProductInfo> scanProduct(String barcode) async {
    // Implement product scanning API call
  }
  
  Future<List<RecentScan>> getUserScans(String userId) async {
    // Implement user scans retrieval
  }
  
  Future<UserProfile> updateUserProfile(UserProfile profile) async {
    // Implement profile update
  }
}
```

---

## ✅ Testing Guidelines

### Unit Tests
- Test all business logic functions
- Test data models serialization/deserialization
- Test utility functions and validators

### Widget Tests
- Test all custom widgets in isolation
- Test user interactions and state changes
- Test responsive layout behavior

### Integration Tests
- Test complete user flows (onboarding, scanning, etc.)
- Test navigation between screens
- Test data persistence and retrieval

---

## 🚀 Deployment Checklist

### Pre-deployment
- [ ] Test on multiple screen sizes
- [ ] Test on both iOS and Android
- [ ] Verify all animations are smooth
- [ ] Check accessibility compliance
- [ ] Test offline functionality
- [ ] Validate API integration
- [ ] Test performance with large datasets

### App Store Requirements
- [ ] App icons for all required sizes
- [ ] Launch screen/splash screen
- [ ] Privacy policy and terms of service
- [ ] App Store screenshots and descriptions
- [ ] Proper app permissions handling

---

This specification provides a complete blueprint for implementing the SmartLabelScan app in Flutter. Each section contains detailed implementation guidance, code examples, and best practices to ensure a smooth development process.