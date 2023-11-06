# hw2
## 圖片
[![圖片](https://github.com/MKE0108/1103329-swift/blob/main/hw3/A.PNG?raw=true)]
[![圖片](https://github.com/MKE0108/1103329-swift/blob/main/hw3/B.PNG?raw=true)]
```swift

import SwiftUI

struct titleView: View {
    var name:String
    var sys:String
    var body: some View {
        VStack(){
            Image(systemName: sys)
                .imageScale(.large)
                .foregroundColor(.accentColor)
            Text(name).font(.largeTitle).padding(.bottom,10)
        }.frame(maxWidth: .infinity,alignment: .center).padding(.top,20).background(.red.opacity(0.3))
    }
}

struct itemView: View {
    var imageName:String
    var imagetitle:String
    var body: some View {
        VStack(alignment: .center){
            Image("\(imageName)").resizable()
                .resizable().aspectRatio( contentMode:.fit).frame(height: UIScreen.screenHeight/10,alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/).padding(/*@START_MENU_TOKEN@*/10/*@END_MENU_TOKEN@*/).shadow(color: .black, radius: 10, x: 0, y: 4)
            Text(imagetitle.capitalized)
                .fontWeight(/*@START_MENU_TOKEN@*/.bold/*@END_MENU_TOKEN@*/).font(.system(size:15))
        }.frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, minHeight: 0, idealHeight: 100, maxHeight: 200, alignment: .center).background(Color.mint.opacity(0.3))
    }
}
struct WideitemView: View {
    var imageName:String
    var imagetitle:String
    var body: some View {
        ZStack(alignment: .center){
            Image(imageName)
                .resizable().aspectRatio( contentMode:.fit).frame(height:UIScreen.screenHeight/3.7, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/).shadow(color: .black, radius: 10, x: 0, y: 4).offset(y:-10)
            Text(imagetitle)
                .fontWeight(/*@START_MENU_TOKEN@*/.bold/*@END_MENU_TOKEN@*/).font(.system(size:15)).offset(x:90,y:90)
        }.frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, maxHeight: 200,alignment: .center).background(.blue.opacity(0.3))
    }
}


struct LongitemView: View {
    var imageName:String
    var imagetitle:String
    var body: some View {
        VStack(alignment: .center){
            Image(imageName)
                .resizable().aspectRatio( contentMode:.fit).frame(width: UIScreen.screenWidth/9.5, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/).shadow(color: .black, radius: 10, x: 0, y: 4)
            Text(imagetitle)
                .fontWeight(/*@START_MENU_TOKEN@*/.bold/*@END_MENU_TOKEN@*/).font(.system(size:15)).offset(x:-3,y:13)
        }.frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity,maxHeight: 410, alignment: .center).background(Color.indigo.opacity(0.5))
    }
}
struct item:Identifiable{
    var id = UUID()
    var path:String
    var name:String
}
struct firstView:View{
    var titlename:String
    var sys:String
    var items:[item]
    var body: some View{
        VStack{
             titleView(name: titlename, sys: sys)
        VStack{
            Spacer()
            VStack{
                VStack{
                }.frame(height: 0.5)
                HStack{
                    ForEach(items.prefix(3)) { item in
                        itemView(imageName: item.path,imagetitle: item.name)                    
                    }
                }
                HStack{
                    ForEach(items.suffix(3)) { item in
                        itemView(imageName: item.path,imagetitle: item.name)                    
                    }
                }
                VStack{
                }.frame(height: 0.5)
            }.background(.gray)
            Spacer()
            
        }.frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, alignment: .center)
      }
    }
    
}
struct secondView:View{
    var titlename:String
    var sys:String
    var items:[item]
    var body: some View{
        VStack{
            titleView(name: titlename, sys: sys)
            Spacer()
            VStack{
                VStack{
                }.frame(height: 0.5)
                HStack{
                    VStack{
                        ForEach(items.prefix(2)) { item in
                            itemView(imageName: item.path,imagetitle: item.name)       
                        }
                    }
                    LongitemView(imageName: items[2].path,imagetitle: items[2].name)     
                }
                WideitemView(imageName: items[3].path,imagetitle: items[3].name)
                VStack{
                }.frame(height: 0.5)
            }.background(.gray)
          Spacer()
        }
    }
    
}
struct ContentView: View {
    var items1:[item]=[item(path:  "A", name: "帝王決"),item(path:  "B",name: "紫青雙劍錄"),item(path:  "c",name: "古龍驚魂"),item(path:  "d",name: "古龍真品"),item(path:  "e",name: "馬踏天下"),item(path:  "f",name: "【魔法童話】"),]
    var items2:[item]=[item(path:  "2A", name: "Saber"),item(path:  "2B",name: "馬修"),item(path:  "2D",name: "Saber&士郎"),item(path:  "2E",name: "梅柳齊娜")]
    var body: some View {
        TabView {
            firstView(titlename:"書櫃",sys: "books.vertical.fill",items: items1)
                .tabItem {
                    Label("書櫃", systemImage: "books.vertical.fill")
                }
            
            secondView(titlename:"模型",sys: "textformat.size.larger.ja",items: items2)
                .tabItem {
                    Label("模型", systemImage: "textformat.size.larger.ja")
                }
        }
    }
}


extension UIScreen{
    static let screenWidth = UIScreen.main.bounds.size.width
    static let screenHeight = UIScreen.main.bounds.size.height
    static let screenSize = UIScreen.main.bounds.size
    
}
#Preview{
    ContentView()
}



```
