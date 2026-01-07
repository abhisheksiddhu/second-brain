## PHASE 1: MVP SCREENS

### Authentication & Onboarding

1. Splash Screen - App logo/branding while loading
2. Welcome/Intro Screen - First-time user introduction (optional carousel)
3. Login Screen - Email/password with demo credentials (as shown)
4. Forgot Password Screen - Email input for password reset
5. Reset Password Screen - New password entry
6. Password Reset Success Screen - Confirmation message
7. Sign Up - Role Selection - Choose: Parent or Coach
8. Sign Up - Parent Form - Name, email, password, phone
9. Sign Up - Coach Form - Basic info, specializations
10. Sign Up - Verification - Email/phone OTP verification
11. Sign Up - Success Screen - Welcome message

---

### PARENT/CLIENT SCREENS

#### Home & Discovery

12. Home Screen (Parent) - Welcome, search, categories, recommendations (Screenshot 5)
13. Search/Find Coaches Screen - List View - Filtered coach list (Screenshot 6)
14. Search/Find Coaches Screen - Map View - Coaches plotted on map
15. Filter & Sort Screen - Distance, price, rating, availability, categories
16. Category View Screen - Browse coaches by category (Sports, Music, Academic, Life Skills)
17. Coach Profile Screen - Full details, about, services, schedule, reviews (Screenshot 3)
18. Coach Reviews Screen - All reviews with ratings
19. Coach Services Tab - List of offered services/specializations
20. Coach Schedule Tab - Availability calendar view
21. Share Coach Profile Screen - Share via deeplink options
22. Favorite Coaches Screen - Saved/bookmarked coaches list

#### Booking Flow

23. Book Session - Schedule Step - Select date, time, duration (Screenshot 4)
24. Book Session - Details Step - Session type, location, special requests
25. Book Session - Payment Step - Payment method selection, card entry (most probably stripe or similar payment gateway integration)
26. Book Session - Payment Processing - Loading/processing screen
27. Book Session - Confirm Step - Review all details before booking
28. Booking Success Screen - Confirmation with booking details
29. Booking Failure Screen - Error message with retry options

#### My Bookings

30. My Bookings Screen - Upcoming Tab - Confirmed upcoming sessions (Screenshot 2)
31. My Bookings Screen - Past Tab - Completed sessions
32. My Bookings Screen - Cancelled Tab - Cancelled bookings
33. Booking Details Screen - Full details of a specific booking
34. Reschedule Booking Screen - Select new date/time
35. Cancel Booking Screen - Cancellation reason, policy, confirmation
36. Cancellation Success Screen - Confirmation message

#### Messaging

37. Messages List Screen - All conversations, unread, archived (Screenshot 7)
38. Message Thread Screen - 1-on-1 conversation with coach
39. New Message Screen - Start conversation with a coach

#### Profile & Settings

40. Parent Profile Screen - View/edit personal info
41. Edit Profile Screen - Update name, email, phone, photo
42. Payment Methods Screen - Saved cards, add/remove payment methods
43. Add Payment Method Screen - Stripe card input
44. Transaction History Screen - Past payments, receipts
45. Settings Screen - General app settings
46. Notification Settings Screen - Push notification preferences
47. Privacy Settings Screen - Data preferences
48. Help & Support Screen - FAQs, contact support (static for MVP)
49. Terms & Conditions Screen - Legal text (static)
50. Privacy Policy Screen - Legal text (static)
51. About App Screen - Version info, other company info (static)

---

### COACH SCREENS

#### Dashboard & Overview

52. Coach Dashboard/Home Screen - Stats, today's schedule (Screenshot 8)
53. Coach Analytics Screen (Optional detail view) - Extended earnings/session metrics

#### Schedule & Availability

54. Coach Schedule Screen - Weekly/monthly calendar view
55. Add Availability Screen - Set available time slots
56. Edit Availability Screen - Modify existing availability
57. Availability Settings Screen - Recurring availability patterns
58. Today's Schedule Screen - Detailed view of today's sessions

#### Bookings Management

59. Coach Bookings Screen - Upcoming Tab - Confirmed sessions
60. Coach Bookings Screen - Past Tab - Completed sessions
61. Coach Bookings Screen - Pending Tab - Requests awaiting confirmation
62. Coach Booking Details Screen - Full session details
63. Accept/Decline Booking Screen - Respond to booking requests
64. Reschedule Request Screen - Propose new time to client

#### Earnings & Payments

65. Earnings Dashboard Screen - Total, pending, paid earnings
66. Earnings Detail Screen - Breakdown by session
67. Payout Settings Screen - Bank account setup (Stripe Connect)
68. Payout History Screen - Past withdrawals/transfers
69. Request Payout Screen - Withdraw available balance

#### Coach Profile & Services

70. Coach Profile View (Self) - How others see your profile
71. Edit Coach Profile Screen - Update bio, photo, specializations
72. Manage Services Screen - Add/edit/remove services offered
73. Add Service Screen - Service name, description, pricing
74. Edit Service Screen - Modify existing service
75. Pricing Settings Screen - Set hourly rates by service type

#### Messaging

76. Coach Messages List Screen - Conversations with clients
77. Coach Message Thread Screen - 1-on-1 with client
78. New Message to Client Screen - Initiate conversation

#### Coach Settings

79. Coach Settings Screen - Account settings
80. Coach Notification Settings - Booking alerts, messages
81. Coach Privacy Settings - Profile visibility options

---

### NOTIFICATIONS

82. Notifications Screen - All app notifications (bookings, messages, reminders)
83. Notification Detail Screen - Expanded notification with actions

---

### GENERAL/SHARED SCREENS

84. No Internet Connection Screen - Offline state
85. Error Screen - Generic error handling
86. Loading/Skeleton Screens - For list views while fetching data
87. Empty State Screens - No bookings, no messages, no favorites, etc.
88. Logout Confirmation Screen - Confirm before logging out

---

## PHASE 2: SECONDARY/OPTIONAL SCREENS

### Advanced Analytics (Coach)

89. Performance Analytics Screen - Client retention, session trends
90. Revenue Analytics Screen - Monthly/yearly earnings graphs
91. Client Insights Screen - Most active clients, feedback trends

### Session Management

92. Session Check-In Screen - Mark session as started
93. Session Check-Out Screen - Mark session as completed
94. Session Notes Screen - Add notes after session
95. Session Progress Tracker - Track client progress over time
96. Progress Reports Screen - View client improvement

### Reviews & Ratings

97. Leave Review Screen - Rate and review after session
98. Review Submitted Success - Confirmation
99. Report Review Screen - Flag inappropriate reviews
100. Review Dispute Screen - Coach disputes a review

### Referral Program

101. Referral Dashboard Screen - Track invites and rewards
102. Invite Friends Screen - Share referral code/link
103. Referral Rewards Screen - Earned credits/bonuses

### Onboarding/Tutorial

104. App Tutorial Screen 1 - Swipeable intro slides
105. App Tutorial Screen 2
106. App Tutorial Screen 3
107. Tutorial Skip/Done Screen

### Video/Communication

108. Video Call Screen - In-app video for remote sessions
109. Call Settings Screen - Audio/video preferences
110. Call Ended Screen - Session summary after video call

### File Sharing

111. Shared Files Screen - Documents/media shared in conversations
112. Upload File Screen - Select and upload files
113. View File Screen - Preview documents/images

### Gamification (Future)

114. Achievements Screen - Badges, milestones
115. Leaderboard Screen - Top coaches/active parents

---

## 📊 ESTIMATED SCREEN COUNT

- MVP Screens: ~88 screens
- Secondary Screens: ~27 screens
- Total: ~115 screens

---

## BOTTOM NAVIGATION SUMMARY

### Parent/Client Nav:

- Home
- Search
- Bookings
- Messages
- Profile

### Coach Nav:

- Dashboard
- Bookings
- Messages
- Profile

---

## DESIGN COMPONENTS TO CONSIDER

Beyond full screens, you'll also need:

- Modals/Bottom Sheets: Quick actions, confirmations, filters
- Toast Messages: Success/error notifications
- Pull-to-Refresh: For lists and feeds
- Swipe Actions: Delete messages, archive conversations
- Tab Bars: Within screens (Upcoming/Past/Cancelled)
- Date/Time Pickers: For booking and availability
- Calendar Components: Month/week views
- Rating Components: Star ratings input/display
- Search Bars: With autocomplete
- Filter Chips: Quick filter selections
- Status Badges: Confirmed, Pending, Requires Action
- Avatar/Profile Pictures: With fallback states
- Empty States: Illustrations for no data
- Loading States: Spinners, skeleton screens
- Error States: Retry buttons, error messages
