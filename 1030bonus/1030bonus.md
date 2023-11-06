# hw3
## 圖片
![圖片](https://github.com/MKE0108/1103329-swift/blob/main/1030bonus/A.PNG?raw=true)
```swift
//
//  ContentView.swift
//  1030-1
//
//  Created by MKE on 2023/10/30.
//

import SwiftUI

func formatDate(_ date: Date) -> String {
    let dateFormatter = DateFormatter()
    dateFormatter.dateFormat = "YYYY/MM/dd"
    return dateFormatter.string(from: date)
}
struct ContentView: View {
    let displayFontType = [".default",".rounded",".monospaced",".serif"];
    @State var displayFontSelected = 0
    @State var IsDeepScheme = false
    @State var colorArray:Array = [255.0,255.0,255.0]
    @State var stepperValue = 0
    @State var sliderValue = 0.0
    @State var selectedDate:Date=Date()
    var body: some View{
        
            Form(content: {
                Section(header:Text("文字選擇")){
                    Picker(selection: $displayFontSelected,label:
                            Text("選擇\(displayFontSelected)"
                                )){
                        ForEach(0..<displayFontType.count,id:\.self,content: {
                            Text(self.displayFontType[$0])
                        })
                        
                    }
                }
                Section(header:Text("背景風格")){
                    Toggle(isOn: $IsDeepScheme) {
                        Text("dark(\(String(IsDeepScheme).capitalized))")
                    }
                }
                Section(header:Text("計數器")){
                    Stepper(
                        onIncrement: { stepperValue += 1},
                        onDecrement: { stepperValue -= ((stepperValue>=1) ? 1:0) })
                        {
                            Text("\( stepperValue )")
                        }
                }
                Section(header:Text("滑桿\(sliderValue,specifier: "%.2f")")){
                    Slider(value: $sliderValue,in:0...1)
                }
                Section(header:Text("\(formatDate(selectedDate))")){
                    DatePicker("日期", selection: $selectedDate, displayedComponents: .date)
                        .datePickerStyle( DefaultDatePickerStyle())
                }
            })
            
        }
    
    
        
    }





```
