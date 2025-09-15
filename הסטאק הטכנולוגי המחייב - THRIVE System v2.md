# הסטאק הטכנולוגי המחייב - THRIVE System v2

## מבוא

מסמך זה מגדיר את הסטאק הטכנולוגי המחייב עבור פרויקט THRIVE System v2. כל הפיתוח חייב להתבצע בהתאם לסטאק זה ללא יוצא מן הכלל.

## עקרונות יסוד

### 1. Google Cloud Native בלבד
- כל התשתית חייבת להיות מבוססת על Google Cloud Platform
- אסור להשתמש בשירותי ענן אחרים כפתרון ראשי
- כל הפריסה חייבת להתבצע על Google Cloud

### 2. TypeScript בלבד
- כל הקוד חייב להיות כתוב ב-TypeScript
- אסור להשתמש ב-JavaScript
- חובה לשמור על Type Safety מלא

### 3. ביצועים גבוהים
- זמני תגובה מתחת ל-100ms
- אופטימיזציה מתמדת לביצועים
- שימוש יעיל במשאבי המערכת

## הסטאק המאושר

### Backend Framework
- **Fastify** - Framework יחיד מאושר
- **אסור**: Express.js, Koa, Hapi או כל framework אחר

### API Layer
- **GraphQL** עם Apollo Server
- **אסור**: REST API בלבד, tRPC או פתרונות אחרים

### Database
- **Prisma ORM** - ORM יחיד מאושר
- **Google Cloud SQL** (PostgreSQL) - מסד נתונים ראשי
- **Google Cloud Firestore** - לנתונים בזמן אמת
- **Google Cloud Memorystore** (Redis) - לcaching
- **אסור**: MongoDB, MySQL ישיר, Supabase

### Frontend Framework
- **Next.js 14+** - Framework יחיד מאושר
- **React 18+** - ספריית UI
- **אסור**: Angular, Vue.js, Svelte

### State Management
- **Zustand** - ניהול state יחיד מאושר
- **אסור**: Redux, MobX, Context API לבד

### UI Components
- **Radix UI** + **shadcn/ui** - רכיבי UI מאושרים
- **Tailwind CSS** - עיצוב יחיד מאושר
- **אסור**: Material-UI, Ant Design, Bootstrap

### Runtime Environment
- **Node.js 22+** - גרסה מינימלית
- **אסור**: Deno, Bun או runtime אחר

## Google Cloud Services

### Compute
- **Cloud Run** - לפריסת containers
- **Google Kubernetes Engine (GKE)** - לאורקסטרציה מתקדמת

### Storage
- **Cloud Storage** - אחסון קבצים
- **Cloud SQL** - מסדי נתונים יחסיים
- **Firestore** - מסד נתונים NoSQL
- **Memorystore** - Redis מנוהל

### Security
- **Cloud KMS** - ניהול מפתחות
- **Secret Manager** - ניהול סודות
- **Identity Platform** - אימות משתמשים

### Monitoring
- **Cloud Operations Suite** - ניטור ולוגים
- **Cloud Trace** - מעקב ביצועים
- **Error Reporting** - דיווח שגיאות

## כלי פיתוח

### Containerization
- **Docker** - יחיד מאושר
- **אסור**: Podman או כלים אחרים

### CI/CD
- **GitHub Actions** - יחיד מאושר
- **Cloud Build** - לבניות GCP
- **אסור**: Jenkins, GitLab CI, CircleCI

### Package Management
- **npm** או **pnpm** - מאושרים
- **אסור**: yarn (למעט מקרים מיוחדים)

## טכנולוגיות אסורות

### Frameworks אסורים
- ❌ Express.js
- ❌ Angular
- ❌ Vue.js
- ❌ Svelte
- ❌ Django
- ❌ Flask
- ❌ Ruby on Rails

### Databases אסורות
- ❌ MongoDB
- ❌ Supabase
- ❌ Firebase Realtime Database
- ❌ AWS DynamoDB
- ❌ Azure Cosmos DB

### Cloud Providers אסורים
- ❌ AWS (כפתרון ראשי)
- ❌ Azure (כפתרון ראשי)
- ❌ Vercel
- ❌ Netlify
- ❌ Heroku

### State Management אסור
- ❌ Redux
- ❌ MobX
- ❌ Context API לבד

## דרישות איכות

### Performance
- זמני תגובה API: < 100ms
- זמני טעינה דף: < 2 שניות
- זמני שאילתות DB: < 50ms

### Security
- הצפנה מלאה של כל הנתונים
- אימות דו-שלבי
- HTTPS בלבד

### Scalability
- תמיכה בעד 10,000 משתמשים בו-זמנית
- auto-scaling אוטומטי
- load balancing

## תהליך אישור

### Code Review
- כל PR חייב לעבור סקירה
- בדיקת עמידה בסטאק המחייב
- בדיקת איכות קוד

### Testing
- כיסוי בדיקות מינימלי: 80%
- בדיקות יחידה חובה
- בדיקות אינטגרציה חובה

### Deployment
- פריסה אוטומטית דרך CI/CD
- בדיקות pre-production
- rollback אוטומטי במקרה של כשל

## אכיפה

### אוטומטית
- בדיקות אוטומטיות בכל commit
- דחיית PR שלא עומד בתקנים
- התראות על חריגות מהסטאק

### ידנית
- סקירת קוד מחמירה
- בדיקות איכות תקופתיות
- ביקורת ארכיטקטורה

## עדכונים

מסמך זה מתעדכן באופן תקופתי. כל שינוי בסטאק חייב לעבור אישור מנהל הפרויקט.

**גרסה**: 1.0  
**תאריך עדכון אחרון**: 15 בספטמבר 2025  
**מאושר על ידי**: Manus AI - Project Manager  
**סטטוס**: פעיל ומחייב

