# Question 1
a)
- **Candidate**:
```mermaid
erDiagram
    Candidate {
            int CandidateID
            string Name
            string Number
	        date DOB
        }
```

- **JobHistory**:
```mermaid
erDiagram
    JobHistory {
            int JobHistoryID
            int CandidateID
            string CompanyName
	        string JobTitle
	        date StartDate
        }
```

- **Qualification**:
```mermaid
erDiagram
    Qualification {
            int QualificationID
            string QualificationName
	        date QualifcationAchievedDate
        }
```
- **Company**:
```mermaid
erDiagram
    Company {
            int CompanyID
            string CompanyName
            string Address
	        date Number
        }
```

- **Opening**:
```mermaid
erDiagram
    Opening {
            int OpeningID
            int CompanyID
	        date startDate
        }
```

- **Placement**:
```mermaid
erDiagram
    Placement {
            int PlacementID
			int OpeningID
            int CandidateID
	        date PlacementDate
        }
```

b)

```mermaid
erDiagram
    CANDIDATE {
        int CandidateID PK
        string Name
        string ContactInfo
    }
    JOBHISTORY {
        int JobHistoryID PK
        int CandidateID FK
        string CompanyName
        string JobTitle
        date StartDate
        date EndDate
    }
    QUALIFICATION {
        int QualificationID PK
        string QualificationName
    }
    COMPANY {
        int CompanyID PK
        string CompanyName
        string Address
        string ContactInfo
    }
    OPENING {
        int OpeningID PK
        int CompanyID FK
        string RequiredQualifications
        date StartDate
    }
    PLACEMENT {
        int PlacementID PK
        int OpeningID FK
        int CandidateID FK
        date PlacementDate
    }

    CANDIDATE ||--o{ JOBHISTORY : "has"
    CANDIDATE }o--o{ QUALIFICATION : "earns"
    COMPANY ||--o{ OPENING : "posts"
    OPENING }o--o{ QUALIFICATION : "requires"
    OPENING }o--o{ PLACEMENT : "is filled by"
    CANDIDATE ||--o{ PLACEMENT : "fills"

```


c)

```mermaid
erDiagram
    CANDIDATE {
        int CandidateID PK
        string Name
        string ContactInfo
    }
    COMPUTER_SCIENTIST {
        int CandidateID PK, FK
        boolean JavaExperience
    }
    ENGINEER {
        int CandidateID PK, FK
        boolean MatlabExperience
    }
    JOBHISTORY {
        int JobHistoryID PK
        int CandidateID FK
        string CompanyName
        string JobTitle
        date StartDate
        date EndDate
    }
    QUALIFICATION {
        int QualificationID PK
        string QualificationName
    }
    COMPANY {
        int CompanyID PK
        string CompanyName
        string Address
        string ContactInfo
    }
    OPENING {
        int OpeningID PK
        int CompanyID FK
        string RequiredQualifications
        date StartDate
    }
    MONTHLY_PAYMENT_OPENING {
        int OpeningID PK, FK
        float MonthSalary
    }
    HOURLY_PAYMENT_OPENING {
        int OpeningID PK, FK
        float HourSalary
    }
    PLACEMENT {
        int PlacementID PK
        int OpeningID FK
        int CandidateID FK
        date PlacementDate
    }

    CANDIDATE ||--o{ JOBHISTORY : "has"
    CANDIDATE }o--o{ QUALIFICATION : "earns"
    COMPANY ||--o{ OPENING : "posts"
    OPENING }o--o{ QUALIFICATION : "requires"
    OPENING }o--o{ PLACEMENT : "is filled by"
    CANDIDATE ||--o{ PLACEMENT : "fills"

    %% Specialization
    CANDIDATE ||--|{ COMPUTER_SCIENTIST : "is a"
    CANDIDATE ||--|{ ENGINEER : "is a"

    OPENING ||--|{ MONTHLY_PAYMENT_OPENING : "is a"
    OPENING ||--|{ HOURLY_PAYMENT_OPENING : "is a"
```

# Question 2


a)

6 authors in total:
min of 6
max of 12

An author can be associated with 1 or 2 books
A book can be written by 1 to 3 authors

min: 6 readers
max: 60 readers

b)

- **Minimum Number of Books**: 6
- **Maximum Number of Books**: 30
- **Minimum Number of Authors**: 6
- **Maximum Number of Authors**: 15


# Question 3
a)
```mermaid
erDiagram
    STUDENT {
        int StudentID PK
        string Name
        string Grade
        string Gender
    }
    
    CRUSH {
        int CrushID PK
        int Duration
        int StudentID FK
    }
    
    STUDENT ||--o| CRUSH : "has a crush on"

```

b)

```mermaid
erDiagram
    STUDENT {
        int StudentID PK
        string Name
        string Grade
    }
    
    BOY {
        int StudentID PK, FK
    }
    
    GIRL {
        int StudentID PK, FK
    }
    
    CRUSH {
        int CrushID PK
        int Duration
        int StudentID FK
    }
    
    STUDENT ||--o| BOY : "is a"
    STUDENT ||--o| GIRL : "is a"
    
    BOY ||--o| CRUSH : "has a crush on"
    GIRL ||--o| CRUSH : "is crushed on by"

```
