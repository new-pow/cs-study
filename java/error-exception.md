# π£Β νλ‘κ·Έλ¨μ μ€λ₯

νλ‘κ·Έλ¨μ μΈ κ°μ§λ‘ λλ  μ μλ€.

- **μ»΄νμΌ μλ¬** (compile-time error) μ»΄νμΌ ν  λ λ°μνλ μλ¬
- **λ°νμ μλ¬** (runtime error) μ€νν  λ λ°μνλ μλ¬
- **λΌλ¦¬μ  μλ¬** (logical error) μμ± μλμ λ€λ₯΄κ² λμ

## μ»΄νμΌ μλ¬

- λ¬Έλ²μ  μ€λ₯κ° λ°μν  λ μ»΄νμΌ μλ¬κ° λ°μνλ€.

```java
system.out.println("Hello world!");
```

- μ»΄νμΌ ν  λ μ΄λ€ μλ¬κ° λ°μνλμ§ μλ €μ€λ€.
- class νμΌμ΄ λ§λ€μ΄μ§μ§ μλλ€.

<aside>
π©π»βπ» μ°Έμ‘° : μ»΄νμΌλ¬κ° νλ μΌ
- κ΅¬λ¬Έ μ²΄ν¬
- λ²μ­
- μ΅μ ν
- μλ΅λ μ½λ μΆκ° : `extends Object` λ±

</aside>


## λ°νμ μλ¬

- μ€ν μ€ λ°μνλ μλ¬
- λ€μν μλ¬κ° λ°μνλ€.
- IDEκ° λ³΄μ‘°νμ¬ μλ €μ€λ€.
- μ€ννλ€ λ°μνλ©΄ νλ‘κ·Έλ¨μ΄ μ’λ£λλ€.
- λ°νμ μλ¬μ μ’λ₯ : μλ¬errorμ μμΈexception
    - **error** : νλ‘κ·Έλ¨ μ½λμ μν΄μ μμ΅λ  μ μλ μ¬κ°ν μ€λ₯. κ°λ°μκ° λ―Έλ¦¬ μμΈ‘νμ¬ λ°©μ§ν  μ μλ€. (OutOfMemory error λ±)
    - **exception** : νλ‘κ·Έλ¨ μ½λμ μν΄μ μμ΅λ  μ μλ λ€μ λ―Έμ½ν μ€λ₯. κ°λ°μκ° κ΅¬νν λ‘μ§μμ λ°μν μ€μλ μ¬μ©μμ μν₯μ μν΄ λ°μ. κ°λ°μκ° λ―Έλ¦¬ μμΈ‘νμ¬ λ°©μ§ν  μ μλ€.
- μλ¬λ μ΄μ© μ μμ§λ§, μμΈλ μ²λ¦¬νμ.

## λΌλ¦¬μ  μλ¬

- νλ‘κ·Έλ¨μ μ μνμ΄ λλ, μλμ λ€λ₯΄κ² λμν  λ

---

# π οΈΒ Error & Exception ν΄λμ€ κ΅¬μ‘°

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4dd0c5f6-41f3-4dc2-b220-a25d55b38d6b%2FUntitled.png?id=0f6a4671-60c5-48a5-a3a6-e51b90358500&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- Throwable : ν΄λμ€, λͺ¨λ  μ€λ₯μ μ‘°μ
- Exception : λ°νμμλ¬ μ€ λ―Έμ½ν μ€λ₯
- Error : λ°νμμλ¬ μ€ μ¬κ°ν μ€λ₯

## Throwable??

- μ€λ₯μ μμΈ λͺ¨λ μλ° μ΅μμ ν΄λμ€ Objectμ μμμ λ°λλ€.
- κ·Έ μ¬μ΄ `Throwable` ν΄λμ€κ° μλλ°, μ€λ₯λ μμΈμ λν λ©μμ§λ₯Ό λ΄λ λ©μλμ μμΈκ° μ°κ²°λ  λ(chained exception) μ°κ²°λ μμΈ μ λ³΄λ€μ κΈ°λ‘νκ³  μΆλ ₯νλ λ©μλλ₯Ό κ°μ§λ€.
    - `getMessage()`
    - `printStackTrace()`

## Checked Exception - Unchecked Exception

### μ²΄ν¬ μμΈ Checked Exception

- RuntimeException ν΄λμ€ μΈ Exceptionμ μμλ€
- λ°λμ μλ¬ μ²λ¦¬λ₯Ό ν΄μΌνλ€. (try/catch or throw)
- μ¬μ©μμ μ€μμ κ°μ μΈμ μΈ μμΈμ μν΄ λ°μνλ μμΈ
    - μμΆλ ₯ μμΈ
    - νμΌμ μ°Ύμ§ λͺ»νλ κ²½μ°
    - μ΄λ¦μ΄ μλͺ»λμ΄ ν΄λμ€ μ°Ύμ§ λͺ»νλ κ²½μ° λ±


### μΈμ²΄ν¬ μμΈ Unchecked Exception

- RuntimeExceptionκ³Ό κ·Έ μμλ€
- λ°λμ μλ¬ μ²λ¦¬λ₯Ό κ°μ νμ§ μλλ€.
- μ€νμ€μ λ°μν  μ μλ μμΈλ₯Ό μλ―Ένλ€.
- νλ‘κ·Έλλ¨Έμ μ€μλ‘ λ°μνλ μμΈ
    - μ°μ  κ³μ°ν  λ μμΈ (5/0)
    - νλ³ν μμΈ
    - nullPoint μμΈ
    - IndexOutOfBounds μμΈ(λ°°μ΄ λ²μ λ²μ΄λ¨)

|  | μ²΄ν¬ μμΈ | μΈμ²΄ν¬ μμΈ |
| --- | --- | --- |
| μμΈμ²λ¦¬ μ¬λΆ | λ°λμ μμΈ μ²λ¦¬ν΄μΌν¨ | λͺμμ μΈ μ²λ¦¬λ₯Ό κ°μ νμ§ μμ |
| νμΈ μμ  | μ»΄νμΌ λ¨κ³ | μ€νλ¨κ³ |
- [μ°Έκ³ μμ : ****μλ° κ³΅λΆλ₯Ό μ΄λ»κ² νκΈΈλ, "μΈμ²΄ν¬λ μμΈ λ°μμ νΈλμ­μ λ‘€λ°±?"****](https://youtu.be/_WkMhytqoCc)

## μμΈ ν΄λμ€μ κ³μΈ΅ κ΅¬μ‘°

- μ μ²΄ μ’λ₯ [Exceptionκ³Ό ErrorΒ μ’λ₯μ λ°μ μμΈ](https://www.notion.so/Exception-Error-0dde35de4d54490ca0ba7aba7090cadf)

![[https://www.atatus.com/blog/types-of-exceptions-in-java/](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8d552bba-31bb-411c-b3b0-652b360a3bd8%2FUntitled.png?id=f62d37fc-b5b0-4ad0-9f77-aad3cc26ac26&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[https://www.atatus.com/blog/types-of-exceptions-in-java/](https://www.atatus.com/blog/types-of-exceptions-in-java/)

| Basis of Comparison | Exception | Error |
| --- | --- | --- |
| Recoverable/ Irrecoverable | try-catch λΈλ‘μΌλ‘ μ²λ¦¬ν  μ μλ€. | μ»€λ²κ° λΆκ°λ₯ |
| Type | checked μ uncheckedλ‘ λλλ€. | λͺ¨λ unchecked error |
| Occurrence | compile timeμ΄λ run timeμμ λ°μνλ€. | run timeμμ λ°μνλ€. |
| Package | java.lang.Exception package | java.lang.Error package |
| Known or unknown | μ²΄ν¬ μμΈλ§ compilerμ μλ €μ§. | Errors will not be known to the compiler. |
| Causes | λλΆλΆ application μ μν΄ λ°μ | λλΆλΆ application μ νκ²½μ μν΄ λ°μ |
| Example | Checked Exceptions:SQLException, IOExceptionUnchecked Exceptions:ArrayIndexOutOfBoundException, NullPointerException, ArithmaticException | Java.lang.StackOverFlow, java.lang.OutOfMemoryError |

[https://www.javatpoint.com/exception-vs-error-in-java](https://www.javatpoint.com/exception-vs-error-in-java)

# π οΈΒ μμΈ μ²λ¦¬ exception handling

- μ μ : νλ‘κ·Έλ¨ μ€νμ λ°μν  μ μλ μμΈ λ°μμ λλΉν μ½λλ₯Ό μμ±νλ κ²
- λͺ©μ  : **νλ‘κ·Έλ¨μ λΉμ μ μ’λ£**λ₯Ό λ§κ³ , μ μμ μΈ μ€νμνλ₯Ό μ μ§νλ κ²

## μμΈκ° μ£Όλ‘ λ°μνλ μμΈ

- μ¬μ©μμ μλͺ»λ λ°μ΄ν° μλ ₯
- μλͺ»λ μ°μ°
- κ°λ°μκ° λ‘μ§μ μλͺ» μμ±
- νλμ¨μ΄, λ€νΈμν¬ μ€μλ
- μμ€ν κ³ΌλΆν

## μμΈ μ²λ¦¬ try-catch

```java
try {
	// μμΈ λ°μν  κ°λ₯μ±μ΄ μλ λ¬Έμ₯λ€
} catch (Exception1 e1) {
	// exception1 μ λν μ²λ¦¬ μ½λ
} catch (Exception2 e2) {
	// exception2 μ λν μ²λ¦¬ μ½λ
} catch (Exception3 e3) {
	// exception3 μ λν μ²λ¦¬ μ½λ
}
```

- μ£Όμ!! ifλ¬Έκ³Όλ λ¬λ¦¬ `{}`λ₯Ό μλ΅ν  μ μλ€.
- try λΈλ­ λ΄μμ μμΈκ° λ°μνλ€λ©΄?
    1. μΌμΉνλ μμΈ `catch` λΈλ­μ΄ μλ μ§ νμΈ
    2. μλ€λ©΄, `catch` λΈλ­ λ΄μ μ½λλ₯Ό μννκ³ , `try-catch`λ₯Ό λΉ μ Έλκ° λ€μ λ¬Έμ₯λΆν° μννλ€.
    3. μλ€λ©΄, μμΈλ μ²λ¦¬λμ§ λͺ»νλ€.
- try λΈλ­ λ΄μμ μμΈκ° λ°μνμ§ μμλ€λ©΄?
    1. `catch` λΈλ­μ κ±°μΉμ§ μκ³  μ μ²΄ `try-catch` λ₯Ό λΉ μ Έλκ° λ€μ λ¬Έμ₯λΆν° μννλ€.
    2. λ§μ½ μ¬λ¬κ° `catch` κ° μμ κ²½μ°, ν΄λΉνλ μμΈμ μ΅μ΄ `catch`λΈλ‘μ μννκ³  λΉ μ Έλμ¨λ€.


## μμΈ κ°μ²΄

### μμΈκ° λ°μνλ©΄ μ΄λ€ μΌμ΄ μΌμ΄λ κΉ?

```java
try {
	int i = 0/0;
} catch (ArithmeticException ae) {
	ae.printStackTrace();
	System.out.println(ae.getMessage());
} catch (Exception e) {
	// exception3 μ λν μ²λ¦¬ μ½λ
}
```

- λ©λͺ¨λ¦¬μ μμΈ κ°μ²΄ μμ±λλ€.
    - μμ μμμμλ `ArithmeticException` νμμΈ κ°μ²΄ μμ±
    - μ°Έμ‘° λ³μ `ae` μ κ°μ²΄ μ£Όμκ° μ μ₯λλ€.
- κ°μ²΄ μμλ μμΈ μ λ³΄κ° λ€μ΄μλ€.
- μμΈ ν΄λμ€ λ©μλλ₯Ό κ°κ³  μλ€. `printStackTrace()`, `getMessage()` λ±...


### μμΈ κ°μ²΄μ λ©μλ

- `printStackTrace()`
    - μμΈ λ°μ λΉμμ νΈμΆ μ€ν(Call Stack)μ μμλ λ©μλμ μ λ³΄μ μμΈ λ©μμ§λ₯Ό νλ©΄μ μΆλ ₯νλ€. λ°νκ°μ void.
- `getMessage()`
    - λ°μν μμΈν΄λμ€μ μΈμ€ν΄μ€μ μ μ₯λ λ©μμ§ String νμμ μ»μ μ μλ€.
- `getStackTrace()`
    - jdk1.4 λΆν° μ§μ, printStackTrace()λ₯Ό λ³΄μ, StackTraceElement[] μ΄λΌλ λ¬Έμμ΄ λ°°μ΄λ‘ λ³κ²½ν΄μ μΆλ ₯νκ³  μ μ₯νλ€.

## finally

- νλ‘κ·Έλ¨ μν μ€ μ΄λ€ μμΈκ° λ°μνλλΌλ λ°λμ μ€νλμ΄μΌ νλ λΆλΆμ΄ μλ€λ©΄ μ΄λ»κ² ν κΉ?

```java
try {
	int i = 0/0;
} catch (ArithmeticException ae) {
	ae.printStackTrace();
	System.out.println(ae.getMessage());
} catch (Exception e) {
	// exception3 μ λν μ²λ¦¬ μ½λ
} finally {
	// μμΈμ μκ΄μμ΄ λ¬΄μ‘°κ±΄ μνλλ μ½λ
}
```

---

# π₯Β μμΈ λ°μμν€κΈ°

- μ κ·Ήμ μΌλ‘ μμΈλ₯Ό λ°μμν¬ μ μλ€.

### λ°©λ²1. `RuntimeException` μ μμλ°μ μμΈλ₯Ό κ΅¬ννλ€.

- `RuntimeException` : νλ‘κ·Έλ¨ μ€νμ λ°μνλ μμΈ

```java
class FoolException extends RuntimeException {
}

public class Sample {
    public void sayNick(String nick) {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

### λ°©λ²2. `Exception` μ μμλ°μ κ΅¬ννλ€.

- `Exception` μ μ»΄νμΌ μ λ°μνλ μμΈμ΄λ€.
- μμ κ°μ μμμλ μ»΄νμΌ μ€λ₯κ° λ°μνλ€.
    - μλμ²λΌ try-catch κ΅¬λ¬ΈμΌλ‘ μ²λ¦¬νλ©΄ μ»΄νμΌ μ€λ₯λ₯Ό λ§μ μ μλ€.
- `sayNick` λ©μλμμ `FoolException`μ λ°μμν€κ³  μμΈμ²λ¦¬λ `sayNick` λ©μλμμ νλ€.

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) {
        try {
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
        }catch(FoolException e) {
            System.err.println("FoolExceptionμ΄ λ°μνμ΅λλ€.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

---

# βΎοΈ μμΈ λμ§κΈ° throws

- μμΈ μ²λ¦¬ ννΌλΌκ³ λ νλ€.
- `sayNick` μ νΈμΆν κ³³μμ `FoolException` μ μ²λ¦¬νλλ‘ μμΈλ₯Ό μλ‘ λμ§ μ μλ λ°©λ²
- throws λΌλ κ΅¬λ¬Έμ λ©μλ λ·λΆλΆμ μ½μνμ¬ νΈμΆν κ³³μΌλ‘ μλ‘ λ³΄λΌ μ μλ€.
- βμμΈλ₯Ό λ€λ‘ λ―Έλ£¬λ€β λΌκ³ λ νλ€.
- μ΄μ  μμΈλ₯Ό μ²λ¦¬ν΄μΌ νλ λμμ΄ sayNick λ©μλμμ main λ©μλλ‘ λ³κ²½λμλ€.

```java
public class Sample {
    public void sayNick(String nick) throws FoolException {
        try {   // try .. catch λ¬Έμ μ­μ ν μ μλ€.
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
        }catch(FoolException e) {
            System.err.println("FoolExceptionμ΄ λ°μνμ΅λλ€.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

- λ€μκ³Ό κ°μ΄ λ³κ²½νλ€.

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) throws FoolException {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        try {
            sample.sayNick("fool");
            sample.sayNick("genious");
        } catch (FoolException e) {
            System.err.println("FoolExceptionμ΄ λ°μνμ΅λλ€.");
        }
    }
}
```

## π€ μμΈ μ²λ¦¬, μ΄λμ νλκ² μ’μκΉ?

- μμ μμμ κ°μ΄ νΈμΆλ λ©μλμμ μ§μ  μμΈ μ²λ¦¬λ₯Ό ν  μλ μκ³ , μλλ©΄ νΈμΆν κ³³μΌλ‘ λμ Έ mainμμ μμΈμ²λ¦¬λ₯Ό ν  μλ μλ€. κ³Όμ° μ΄λμ νλ κ²μ΄ μ’μκΉ?
- λ λ°©λ²μ μ°¨μ΄μ μλ βμ΄λκΉμ§ μ½λλ₯Ό μ€νν  κ²μΈκ°βλΌλ λ¬Έμ κ° κ±Έλ €μλ€.
1. λ©μλ λ΄μμ μμΈμ²λ¦¬ν  κ²½μ°

```java
public class Sample {
    public void sayNick(String nick)  {
        try {
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
        }catch(FoolException e) {
            System.err.println("FoolExceptionμ΄ λ°μνμ΅λλ€.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious"); // μ¬κΈ°κΉμ§ μννλ€.
    }
}
```

```
// output
FoolExceptionμ΄ λ°μνμ΅λλ€.
FoolExceptionμ΄ λ°μνμ΅λλ€.
```

1. Main μμ μμΈμ²λ¦¬λ₯Ό ν  κ²½μ°

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) throws FoolException {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("λΉμ μ λ³λͺμ "+nick+" μλλ€.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        try {
            sample.sayNick("fool"); // μ΄κ²μ μννλ€κ° catchλ‘ λΉ μ§λ€.
            sample.sayNick("genious");
        } catch (FoolException e) {
            System.err.println("FoolExceptionμ΄ λ°μνμ΅λλ€.");
        }
    }
}
```

```
// output
FoolExceptionμ΄ λ°μνμ΅λλ€.
```

- μ΄λ¬ν μ΄μ λ‘ μμΈ μ²λ¦¬ μμΉκ° λ§€μ° μ€μνλ€.
- νλ‘κ·Έλ¨μ μν μ¬λΆλ₯Ό κ²°μ νκ³ , νΈλμ­μκ³Όλ λ°μ ν κ΄κ³κ° μλ€.
    - μ°Έκ³  : [νΈλμ­μ Transaction](https://www.notion.so/Transaction-fffe0b721c97453990841c069af58a06)

---

# μ°κ²°λ μμΈ chained exception

- νΉμ  μμΈμμ λ€λ₯Έ μμΈλ₯Ό λ°μμν€λ κ²
- AμμΈμμ BμμΈ μ²λ¦¬ λΈλ‘μΌλ‘ μ λν  μ μλ€.
- μμΈ μ νμ΄λΌκ³ λ νλ€.

## μ°κ²°λ μμΈλ₯Ό μ μ¬μ©νλ?

- μ²΄ν¬ μμΈλ₯Ό RuntimeExceptionμΌλ‘ κ°μΈ μΈμ²΄ν¬ μμΈλ‘ λ°κΏ μ μλ€.
- μ΄ κΈ°λ₯μ μ¬μ©ν΄ λμ΄μ μ΅μ§λ‘ try-catchλ‘ μ²λ¦¬ν΄μ€ νμκ° μμ΄μ§λ€.
    - μλ μμμμ `MemoryException` λ λ¬΄μ‘°κ±΄ `try-catch` ν΄μ€μΌ νλλ°, μ΄λ μ¬μ€μ μ½λλ‘ μ²λ¦¬ν  μ μμ΄ μλ―Έμλ `catch` κ° λλ€.
    - μ΄λ₯Ό `RuntimeException` μΌλ‘ wrapping νμ¬ λΆνμν `catch` λΈλ­μ μ­μ ν  μ μλ€.

```java
try{
    startInstall();
    copyFiles();
}catch(SpaceException ex){
    InstallException ie = new InstallException("μ€μΉμ€ μμΈ λ°μ");
    ie.initCause(ex);
    throw new RuntimeException(ie);
}
/*catch (MemoryException me){
    //....
}*/
```

### λ°©λ²

1. μ°κ²°ν  μλ‘μ΄ μμΈ κ°μ²΄ μμ±νλ€.
2. μλ‘μ΄ μμΈκ°μ²΄μ `initCause` λ©μλμ μΈμκ°μΌλ‘ κΈ°μ‘΄ μ°κ²°λ  μμΈ κ°μ²΄λ₯Ό λ£μ΄μ€λ€.
    1. `initCause` λ `Trowable` μ μ μλμ΄ μλ λ©μλμ΄λ€.
3. `throw` λ‘ μ°κ²°ν  μμΈ κ°μ²΄λ₯Ό λμ§λ€.

---

# π μμΈ μ²λ¦¬ λ°©λ²

- μΌλ°μ μΈ μμΈ μ²λ¦¬μ λ°©λ² 3κ°μ§
![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1f2395f2-95ac-48bd-822e-bd49e37be284%2FUntitled.jpeg?id=537cf858-0076-4195-b009-5b0a2077156c&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
- μμΈ λ³΅κ΅¬ : λ€λ₯Έ μμ νλ¦μΌλ‘ μ λ
- μμΈμ²λ¦¬ ννΌ : νΈμΆν μͺ½μΌλ‘ λμ§κΈ°
- μμΈ μ ν : νΈμΆν μͺ½μΌλ‘ λμ§ λ λͺνν μλ―Έ μ λ¬μ μν΄ λ€λ₯Έ μμΈλ‘ μ ννμ¬ λμ§κΈ°

## 1. μμΈ λ³΅κ΅¬

```java
int maxretry = MAX_RETRY;
while(maxretry -- > 0) {
    try {
        // μμΈκ° λ°μν  κ°λ₯μ±μ΄ μλ μλ
        return; // μμμ±κ³΅μ λ¦¬ν΄
    }
    catch (SomeException e) {
        // λ‘κ·Έ μΆλ ₯. μ ν΄μ§ μκ°λ§νΌ λκΈ°
    } 
    finally {
        // λ¦¬μμ€ λ°λ© λ° μ λ¦¬ μμ
    }
}
throw new RetryFailedException(); // μ΅λ μ¬μλ νμλ₯Ό λκΈ°λ©΄ μ§μ  μμΈ λ°μ
```

- μμΈκ° λ°μνμ¬λ μ νλ¦¬μΌμ΄μμ μ μμ μΈ νλ¦μΌλ‘ μ§νλλ€.
- μμμ κ²½μ°, μμΈκ° λ°μνλ©΄ κ·Έ μμΈλ₯Ό μΌμ  μκ°λ§νΌλκΈ°νκ³  λ€μ μ¬μλλ₯Ό λ°λ³΅νλ€ μ΅λ μ¬μλ νμλ₯Ό λκΈ°λ©΄ μμΈλ₯Ό λ°μμν¨λ€.
- μ¬μλλ₯Ό ν΅ν΄ μ μμ μΈ νλ¦μ νκ² νλ€κ±°λ, μμΈ λ°μμ λ―Έλ¦¬ μμΈ‘νμ¬ λ€λ₯Έ νλ¦μΌλ‘ μ λμν€λλ‘ κ΅¬ννλ©΄ λΉλ‘ μμΈκ° λ°μνμμ΄λ μ μμ μΌλ‘ μμμ μ’λ£ν  μ μλ€.

## 2. μμΈμ²λ¦¬ ννΌ : μμΈ λμ§κΈ° μ°Έμ‘°

- νΈμΆν μͺ½μμ λ€μ μμΈλ₯Ό λ°μ μ²λ¦¬νλλ‘ νκ±°λ, ν΄λΉ λ©μλμμ μ΄ μμΈλ₯Ό λμ§λ κ²μ΄ μ΅μ μ λ°©λ²μ΄λΌλ νμ μ΄ μμ λλ§ μ¬μ©νλ€.

## 3. μμΈ μ ν : μ°κ²°λ μμΈ μ°Έμ‘°

- νΈμΆν μͺ½μμ μμΈλ₯Ό λ°μμ μ²λ¦¬ν  λ μ’ λ λͺννκ² μΈμ§ν  μ μλλ‘ λκΈ° μν λ°©λ²
- μ΄λ€ μμΈμΈμ§ λΆλͺν΄μΌ μ²λ¦¬κ° μμν΄μ§κΈ° λλ¬Έμ΄λ€.

---

- μ°Έκ³ 
    - μλ°μ μ μ chapter 8
    - [https://movefast.tistory.com/12?category=765934](https://movefast.tistory.com/12?category=765934)
    - [https://mangkyu.tistory.com/152](https://mangkyu.tistory.com/152)
    - [https://www.nextree.co.kr/p3239/](https://www.nextree.co.kr/p3239/)