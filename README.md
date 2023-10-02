# 1103329-swift

![https://github.com/MKE0108/1103329-swift/blob/main/hw1/gcj_star230505.gif?raw=true](https://github.com/MKE0108/1103329-swift/blob/main/hw1/gcj_star230505.gif?raw=true)

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        ScrollView{
            VStack {
                Image("pic") // 
                    .resizable()
                    .frame(width: 150, height: 200, alignment: .trailing)
                    .clipShape(Circle())
                    .padding(.top, 20)
                
                Text("彭康軒") // 替换为您的名字
                    .font(.title)
                    .padding(.top, 10)
                Text("學號:1103329")
                    .font(.subheadline)
                    .foregroundColor(.gray)
                Divider()
                    .padding(.top, 20)
                
                Text("基本資料")
                    .font(.custom("Helvetica Neue", size: 25)).fontWeight(.bold)
                Text("目前在做深度學習和醫療影像的專題")
                    .font(.body)
                    .foregroundColor(.gray)
                    .padding()
                
                Divider()
                    .padding(.top, 20)
            }
            
            
            VStack{
                Text("經歷")
                    .font(.custom("Helvetica Neue", size: 25)).fontWeight(.bold)
                HStack{
                    Text("2018-2021\n2021-2025")
                        .font(.body)
                        .foregroundColor(.gray)
                        .padding()
                    Text("台北市麗山高級中學\n元智大學資訊工程學系")
                        .font(.body)
                        .foregroundColor(.gray)
                        .padding()
                }
                Divider()
                    .padding(.top, 20)
            }
            Text("堅持，直到成功")
                .font(.custom("Helvetica Neue", size: 25)) // 更改座右铭的字体
                .foregroundColor(.gray)
                .padding()
            
            
        }
        
        HStack {
            Spacer()
            VStack{
                Text("") // 替换为您的联系方式
                    .font(.subheadline)
                    .foregroundColor(.gray)
                Text("聯絡方式")
                    .font(.custom("Helvetica Neue", size: 25)).fontWeight(.bold).foregroundColor(.orange)
                HStack {
                    Image(systemName: "phone")
                        .foregroundColor(.green)
                    Text("電話:0928231625") // 替换为您的学号
                        .font(.subheadline)
                        .foregroundColor(.brown)
                }
   
                    HStack {
                        Image(systemName: "envelope.circle")
                            .foregroundColor(.red)
                        // SF Symbol表示联系方式
                        Text("聯絡方式: mickyt711ss@gmail.com") // 替换为您的联系方式
                            .font(.subheadline)
                            .foregroundColor(.brown)
                    }
               
                
                
                Text("") // 替换为您的联系方式
                    .font(.subheadline)
                    .foregroundColor(.gray)
            }
            Spacer()
        }.background(Color.yellow)
        
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
        
    }
}
```
