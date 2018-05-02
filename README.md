# settings_and_resolve_bugs

## Visual Studio

### Оконный проект в Visual Studio C++ (Исключение из HRESULT: 0x8000000A)

Вариант первый 
```sh
Step-1: File-> New -> Projects -> Templates -> visual C++ -> CLR ->Win32 Console Application -> Ok ->Finish
Step-2: RightClick on Source Files -> Add new Items -> Visual C++ -> UI -> Windows Forms (MyForm.h) -> add
Step-3: Click on properties in top-right corner (or) Execute. Done!
```

Вариант второй 
1. закрыть конструктор
2. скомпилировать проект без конструктора
3. открыть конструктор

Вариант третий
1. открыть файл MyForm.cpp и добавить следующай код
```cpp
#include <Windows.h>
using namespace Имя_Вашего_Проекта;
 
int WINAPI WinMain(HINSTANCE, HINSTANCE, LPSTR, int)
{
    Application::EnableVisualStyles();
    Application::SetCompatibleTextRenderingDefault(false);
    Application::Run(gcnew MyForm);
    return 0;
}
```


Вариант четвертый
1. Обозреватель решений -> Проект
2. правым кликом по проекту
3. свойства -> компоновщик -> система -> подсистема -> Windows (/SUBSYSTEM:WINDOWS)
4. свойства -> компоновщик -> дополнительно -> точка входа -> main
5. открыть файл MyForm.cpp (если ее не переименовали) и ввести следующий код :
```cpp
#include "MyForm.h"
using namespace System;
using namespace System::Windows::Forms;
[STAThread]
void main(array<String^>^ args) {
	Application::EnableVisualStyles();
	Application::SetCompatibleTextRenderingDefault(false);
	Имя_вашего_проекта::MyForm form;
	Application::Run(%form);
}
```
6. закрыть и открыть конструктор
