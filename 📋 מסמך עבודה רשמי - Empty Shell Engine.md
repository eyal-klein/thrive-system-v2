# 📋 מסמך עבודה רשמי - Empty Shell Engine
## Work Order #001 - THRIVE SYSTEM Development

**תאריך הוצאה:** 15 ספטמבר 2025  
**רמת עדיפות:** קריטית מקסימלית  
**מנהל פרויקט:** Manus QA Agent  
**מבצע:** אייג'נט התכנות  
**פרויקט:** THRIVE SYSTEM - Empty Shell Architecture  

---

## 🎯 סמכות ניהול

### היררכיה ברורה:
```yaml
project_hierarchy:
  project_manager: "Manus QA Agent"
  authority_level: "SUPREME"
  
  developer: "אייג'נט התכנות"
  authority_level: "EXECUTOR"
  
  reporting_structure:
    - "אייג'נט התכנות מדווח ל-Manus QA Agent"
    - "כל החלטה טכנית דורשת אישור"
    - "דיווח חובה אחרי כל שלב"
    - "אין סטייה מהמפרט ללא אישור"
```

### חובות דיווח:
```yaml
reporting_requirements:
  frequency: "אחרי כל משימה"
  format: "דוח מפורט + קבצים"
  
  must_include:
    - "סטטוס השלמה (הושלם/נכשל/חלקי)"
    - "קבצים שנוצרו/עודכנו"
    - "בעיות שנתקלת בהן"
    - "שאלות או הבהרות נדרשות"
    - "הערכת זמן למשימה הבאה"
  
  escalation:
    - "דווח מיד על כל בעיה חמורה"
    - "אל תמשיך ללא אישור אם יש ספק"
    - "בקש הבהרות במקום לנחש"
```

---

## 🚀 משימה #001: Empty Shell Engine - שלב 1.1

### מטרת המשימה:
יצירת המנוע הבסיסי של Empty Shell Architecture - הליבה שתאפשר יצירת כל הסוכנים במערכת THRIVE.

### רקע טכני:
```yaml
background:
  concept: "Empty Shell Architecture"
  principle: "כל הסוכנים מתחילים כקונטיינרים ריקים"
  loading: "יכולות נטענות דינמית מקסטות"
  
  current_status:
    - "יש קבצי Python של Empty Shell (לא מחוברים)"
    - "צריך לכתוב מחדש ב-TypeScript"
    - "צריך אינטגרציה עם המערכת הקיימת"
```

### דרישות טכניות מחייבות:
```yaml
technical_requirements:
  language: "TypeScript בלבד (אפס JavaScript!)"
  framework: "Fastify (קיים)"
  database: "PostgreSQL + Prisma (קיים)"
  architecture: "100% Google Cloud Native"
  
  compliance:
    - "עמידה ב-THRIVE Stack Authority Document"
    - "אפס טכנולוגיות אסורות"
    - "TypeScript strict mode"
    - "Coherence >= 98%"
```

---

## 📝 משימות מפורטות - שלב 1.1

### משימה 1.1.1: יצירת מבנה התיקיות
```bash
# צור את המבנה הבא:
mkdir -p src/core
mkdir -p src/services/empty-shell
mkdir -p src/routes
mkdir -p cassettes/system
mkdir -p tests/core
```

**דרישות:**
- ודא שהתיקיות נוצרו בנתיב הנכון
- צור קובץ `.gitkeep` בתיקיות ריקות
- דווח על המבנה שנוצר

### משימה 1.1.2: יצירת THRIVEAgent Base Class
```yaml
file: "src/core/THRIVEAgent.ts"
purpose: "הקלאס הבסיסי לכל הסוכנים במערכת"

requirements:
  - "יישום מלא של הקוד שסופק במפרט"
  - "TypeScript strict mode"
  - "JSDoc documentation מלא"
  - "Error handling מקיף"
  - "Event emitter לתקשורת"
  
deliverables:
  - "קובץ THRIVEAgent.ts מלא ופונקציונלי"
  - "Type definitions מלאות"
  - "בדיקת compilation ללא שגיאות"
```

### משימה 1.1.3: יצירת CassetteLoader Service
```yaml
file: "src/core/CassetteLoader.ts"
purpose: "מנוע טעינת וניהול קסטות"

requirements:
  - "יישום מלא של הקוד שסופק"
  - "אינטגרציה עם THRIVEAgent"
  - "Async/await patterns"
  - "Error handling מקיף"
  
deliverables:
  - "קובץ CassetteLoader.ts מלא"
  - "אינטגרציה עם מערכת הקסטות הקיימת"
  - "בדיקת פונקציונליות בסיסית"
```

### משימה 1.1.4: יצירת CoherenceMonitor (Stub)
```yaml
file: "src/core/CoherenceMonitor.ts"
purpose: "ניטור coherence של הסוכנים"

requirements:
  - "יישום stub בסיסי (לא מלא בשלב זה)"
  - "ממשק ברור לפיתוח עתידי"
  - "אינטגרציה עם THRIVEAgent"
  
deliverables:
  - "קובץ CoherenceMonitor.ts עם stub"
  - "Type definitions מוכנות להרחבה"
```

### משימה 1.1.5: עדכון Database Schema
```yaml
file: "prisma/schema.prisma"
purpose: "הוספת טבלאות לניהול Empty Shells"

requirements:
  - "הוספת הטבלאות שסופקו במפרט"
  - "שמירה על התאימות לסכמה הקיימת"
  - "Relations נכונות בין הטבלאות"
  
deliverables:
  - "schema.prisma מעודכן"
  - "הרצת prisma generate בהצלחה"
  - "הרצת prisma db push בהצלחה"
```

---

## ✅ קריטריוני הצלחה

### שלב 1.1 יחשב מושלם כאשר:
```yaml
success_criteria:
  compilation:
    - "כל הקבצים מתקמפלים ללא שגיאות TypeScript"
    - "אין warnings ברמת strict mode"
    
  functionality:
    - "אפשר ליצור instance של THRIVEAgent"
    - "אפשר לטעון קסטה בסיסית"
    - "Database schema עובד"
    
  integration:
    - "אינטגרציה עם המערכת הקיימת"
    - "אין conflicts עם קוד קיים"
    
  documentation:
    - "JSDoc מלא לכל הפונקציות הציבוריות"
    - "README עם הוראות שימוש"
```

---

## 🚨 הוראות חשובות

### אל תעשה:
```yaml
forbidden_actions:
  - "אל תשנה קבצים קיימים ללא אישור"
  - "אל תוסיף dependencies חדשות ללא אישור"
  - "אל תכתוב JavaScript - רק TypeScript"
  - "אל תסטה מהמפרט שסופק"
  - "אל תמשיך למשימה הבאה ללא אישור"
```

### חובה לעשות:
```yaml
mandatory_actions:
  - "דווח אחרי כל משימה משנה"
  - "בקש הבהרות אם משהו לא ברור"
  - "בדוק compilation אחרי כל שינוי"
  - "שמור גיבויים של קבצים שאתה משנה"
  - "כתוב קוד נקי ומתועד"
```

---

## 📊 דוח ביניים נדרש

### אחרי כל משימה משנה, דווח:
```yaml
interim_report_template:
  task_id: "1.1.X"
  status: "הושלם/נכשל/חלקי"
  
  files_created:
    - "רשימת קבצים שנוצרו"
    - "נתיב מלא לכל קובץ"
  
  files_modified:
    - "רשימת קבצים שעודכנו"
    - "תיאור השינויים"
  
  compilation_status:
    - "הצלחה/כישלון"
    - "שגיאות אם יש"
  
  issues_encountered:
    - "בעיות שנתקלת בהן"
    - "פתרונות שיישמת"
  
  questions:
    - "שאלות או הבהרות נדרשות"
  
  next_steps:
    - "מוכן למשימה הבאה/צריך הבהרות"
    - "הערכת זמן למשימה הבאה"
```

---

## 🎯 התחלת העבודה

**אייג'נט התכנות,**

**אתה מתחיל עכשיו במשימה 1.1.1 - יצירת מבנה התיקיות.**

**לאחר השלמת המשימה, דווח לי בפורמט שצוין לעיל.**

**בהצלחה!**

---

**חתימה:**  
**Manus QA Agent**  
**Project Manager - THRIVE SYSTEM**  
**Authority Level: SUPREME**  

---

*מסמך זה מהווה הוראת עבודה רשמית. כל סטייה מהמפרט דורשת אישור מראש מהמנהל.*

