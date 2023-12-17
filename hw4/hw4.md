# hw4
## 影片
[![圖片](https://github.com/MKE0108/1103329-swift/blob/main/hw4/v.PNG?raw=true)](https://youtu.be/goJNM4HeiuM)
## Code
```swift
import SwiftUI
struct ch:Identifiable{
    var id=UUID()
    
    var image:String
    var classes:String
    var name:String
    var jname:String
}

class DollStore: ObservableObject {
    @Published var chsInStore: [ch] = [
        ch(image: "1", classes: "Lancer", name: "斯卡哈", jname: "スカサハ"),
        ch(image: "2", classes: "Saber", name: "阿爾托莉雅·潘德拉貢", jname: "アルトリア・ペンドラゴン"),
        ch(image: "3", classes: "Shielder", name: "瑪修·基利艾拉特", jname: "マシュ・キリエライト"),
        ch(image: "4", classes: "Beast", name: "咕噠子", jname: "ぐだ子"),
    ]
    @Published var myChs: [ch] = [
       
        ch(image: "5", classes: "Lancer", name: "巴托里·伊莉莎白", jname: "エリザベート・バートリー")
    ]
}

struct wellcome: View{
    var body: some View {
        VStack{
            Image("logo")
                .padding(.top, -300) // 减少上方的 padding
            Text("歡迎光臨FGO公仔店！！！").font(.largeTitle).fontWeight(.bold)
                .padding(.bottom,50)
            Text("這裡有賣大量的公仔可供選購～～").font(.title).fontWeight(.regular)
        }
    }
}
struct favorite: View{
    @StateObject var dollData:DollStore
    var body: some View {
        ScrollView(.vertical){
            
                ForEach( dollData.myChs){ c in
                    CardView(image: c.image, classes: c.classes, name: c.name, jname: c.jname)
                }
            
        }.padding(.top,30)
        
    }
}
struct BasicImageRow: View{
    var thisR:ch
    var body: some View {
        HStack{
            Image(thisR.image)
                .resizable().frame(width: 40,height: 60, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/).cornerRadius(10, antialiased: /*@START_MENU_TOKEN@*/true/*@END_MENU_TOKEN@*/)
            Text(thisR.name)
        }
        .padding(10)
    }
}
struct DollDetailText: View {
    var dollName: String // 餐廳名稱變數
    
    var body: some View {
        ScrollView{
            Text("價格：350")
                .font(.largeTitle)
                .padding()
            
        }
    }
}
struct DollDetailView: View {
    @Environment(\.presentationMode) var presentationMode
    @State private var showingPurchaseSuccess = false // 控制 Alert 的显示

    var doll: ch
    var purchaseAction: () -> Void

    var body: some View {
        ScrollView {
            VStack {
                Image(doll.image)
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                    .clipped()
                Text(doll.name)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                    .padding(10)
                Spacer()
                DollDetailText(dollName: doll.name)
                Button("購買") {
                    purchaseAction()
                    self.showingPurchaseSuccess = true
                }
                .padding()
                .buttonStyle(.borderedProminent)
            }
            
        }
        .overlay(
            HStack {
                Spacer()
                VStack {
                    Button(action: {
                        self.presentationMode.wrappedValue.dismiss()
                    }, label: {
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.yellow)
                    })
                    .padding(.trailing, 20)
                    .padding(.top, 10)
                    Spacer()
                }
            }
        )
        .alert(isPresented: $showingPurchaseSuccess) {
            Alert(
                title: Text("購買成功"),
                message: Text("\(doll.name) 已成功加入您的收藏。"),
                dismissButton: .default(Text("ok")) {
                    self.presentationMode.wrappedValue.dismiss()
                }
            )
        }
    }
}


struct store: View {
    @StateObject var dollData:DollStore
    @State private var selectedDoll: ch?
    
    var body: some View {
        
        NavigationView {
            List( dollData.chsInStore) { chs in
                BasicImageRow(thisR: chs).onTapGesture {
                    self.selectedDoll = chs
                }
            }
            .sheet(item: self.$selectedDoll) { doll in
                DollDetailView(doll: doll, purchaseAction: {
                    purchaseDoll(doll)
                    
                })
            }
            .navigationTitle("商品")
        }
        .navigationViewStyle(StackNavigationViewStyle())
    }

    // 购买方法
    private func purchaseDoll(_ doll: ch) {
        if let index =  dollData.chsInStore.firstIndex(where: { $0.id == doll.id }) {
            dollData.myChs.append(doll)
            dollData.chsInStore.remove(at: index)
            
        }
    }
}




























struct ContentView: View {
    @StateObject var dollData = DollStore()

    var body: some View {
        VStack(spacing: 0) {
            HStack {
                Image("icon").resizable().frame(width: 100, height: 100)
                Text("      ")
                Text("公仔店").font(.largeTitle).fontWeight(.heavy).foregroundStyle(.white)
            }
            .frame(maxWidth: .infinity)
            .padding()
            .background(Color.pink)

            TabView {
                Group {
                    wellcome()
                        .tabItem {
                            Label("首頁", systemImage: "house")
                        }

                    favorite(dollData: dollData)
                        .tabItem {
                            Label("我的公仔", systemImage: "textformat.size.larger.ja")
                        }
                    store(dollData: dollData)
                        .tabItem {
                            Label("商店", systemImage: "storefront.fill")
                        }
                }
                .toolbarBackground(Color.black, for: .tabBar)
                .toolbarBackground(.visible, for: .tabBar)
            }
            .tint(.red)
        }
        .edgesIgnoringSafeArea(.top) // Ignore the safe area to extend the red background to the top edge of the screen.
    }
}

struct CardView:View{
    var image:String
    var classes:String
    var name:String
    var jname:String
    var body:some View
    {
       
        VStack{
            Image(image).resizable().aspectRatio(contentMode: .fit)
                .shadow(color: .black, radius: 10, x: 0, y: 4)
                .frame(width: 100).padding(20).padding(.horizontal,100)
                .background(Color(red: 255/255, green: 222/255, blue: 123/255))
            VStack(alignment: .leading, content:
            {
                Text(classes).font(.headline).foregroundStyle(.secondary)
                Text(name).font(.title).foregroundStyle(.primary).lineLimit(3)
                Text(jname).font(.caption).foregroundStyle(.purple)
            }).frame(width:320,height: 100, alignment: .leading)
        }
        .background(Color(red: 255/255, green: 204/255, blue: 153/255))
        .clipShape(.rect(cornerRadius: 20))
        .overlay(RoundedRectangle(cornerRadius:20).stroke(Color.gray, lineWidth: 2)).padding(.all, 10)
    }
}



```
