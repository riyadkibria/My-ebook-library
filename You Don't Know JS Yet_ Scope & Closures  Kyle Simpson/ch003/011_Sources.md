# ch003

## Sources


So we’ve identified all five target references in the program. The other variable references must then be source references (because that’s the only other option!).

In for (let student of students), we said that student is a target, but students is a source reference. In the statement if (student.id == studentID), both student and studentID are source references. student is also a source reference in return student.name.

In getStudentName(73), getStudentName is a source reference (which we hope resolves to a function reference value). In console.log(nextStudent), console is a source reference, as is nextStudent.

What’s the practical importance of understanding targets vs. sources? In Chapter 2, we’ll revisit this topic and cover how a variable’s role impacts its lookup (specifically, if the lookup fails).
