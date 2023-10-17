# hw1

![圖片](https://github.com/MKE0108/1103329-swift/blob/main/hw2/v.MP4?raw=true)

```swift
import SwiftUI
var 剪刀 = "✌️"
var 石頭 = "✊"
var 布 = "🖐️"

struct GameOverView: View {
    @Binding var winner: String
    var restartGame: () -> Void
    
    var body: some View {
        VStack {
            Text("遊戲結束，\(winner)贏了！")
                .font(.title)
                .foregroundColor(.green)
                .padding()
            
            Button(action: {
                restartGame() // 重新開始遊戲
            }) {
                Text("重新開始")
                    .font(.title)
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(10)
            }
        }
    }
}





struct RadomSign: View {
    @State private var currentIndex = 0
    private let options = ["✌️", "✊", "🖐️"]
    
    var body: some View {
        VStack {
            Text(options[currentIndex])
                .font(.largeTitle)
                .padding()
                .background(getBackgroundColor(for: currentIndex))
                .cornerRadius(10)
                .onAppear {
                    startTimer()
                }
        }
    }
    
    func startTimer() {
        Timer.scheduledTimer(withTimeInterval: 0.2, repeats: true) { timer in
            currentIndex = (currentIndex + 1) % options.count
        }
    }
    
    func getBackgroundColor(for index: Int) -> Color {
        switch index {
        case 0:
            return Color.blue.opacity(1)
        case 1:
            return Color.green.opacity(1)
        case 2:
            return Color.red.opacity(1)
        default:
            return Color.clear
        }
    }
}

struct TitleView: View{
    var titlename:String
    var body: some View{
        Text("")
            .font(.title)
        Text(titlename)
            .font(.title)
            .foregroundColor(.white)
            .cornerRadius(5)
            .bold()
    }
}
struct bot: View{
    var botImage:String
    var PrepareState:Bool
    var computerChoice:String
    var body: some View{
        Image(botImage).resizable().frame(width: 200, height: 200, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
        HStack {
            if(PrepareState==true){
                if computerChoice == "剪刀" {
                    
                    Text(剪刀)
                        .font(.largeTitle)
                        .font(.largeTitle)
                        .padding()
                        .background( Color.blue.opacity(1))
                        .cornerRadius(10)
                    
                    
                } else if computerChoice == "石頭" {
                    
                    Text(石頭)
                        .font(.largeTitle)
                        .padding()
                        .background( Color.green.opacity(1))
                        .cornerRadius(10)
                    
                } else if computerChoice == "布" {
                    
                    Text(布)
                        .font(.largeTitle)
                        .padding()
                        .background( Color.red.opacity(1))
                        .cornerRadius(10)
                    
                }
            }else{
                RadomSign()
                
            }
            
            
            
        }.padding(.top, 20)
        
    }
}
struct LifeState:View {
    var leftText:String
    var Health:String
    var LossHealth:String
    var lifebarColor:Color
    var body: some View {
        HStack{
            Text("\(leftText):")
                .font(.title)
                .foregroundColor(.white)
                .cornerRadius(5)
            
            Text("\(Health)\(LossHealth)")
                .padding()
                .font(.title)
                .background(lifebarColor)
                .foregroundColor(.white)
                .cornerRadius(5)
        }
    }
}


struct PlayView: View {
    @State private var PrepareState = false
    @State private var playerChoice = ""
    @State private var computerChoice = ""
    @State private var result = "請選擇一個"
    @State private var playerHealth = "❤️❤️❤️"
    @State private var playerLossHealth = ""
    @State private var computerHealth = "❤️❤️❤️"
    @State private var computerLossHealth = ""
    @State private var isGameEnded = true // 用來跟蹤遊戲是否結束
    @State private var winner = "" // 用來存儲贏家
    @State private var botimagefile = "Picture1"
    @State private var standby = "Picture1"
    @State private var win = "Picture2"
    @State private var loss = "Picture3"
    @State private var showAlert = false
    @State private var alertTitle = ""
    
    var isGameEndedAndNotPrepare: Bool {
        return isGameEnded && !PrepareState
    }
    

    var body: some View {
        VStack{
            TitleView(titlename: "剪刀✌️石頭✊布🖐️")
            ZStack {
                Rectangle()
                    .fill(Gradient(colors: [.gray,.yellow,.gray]))
                    .ignoresSafeArea()
                    .opacity(0.9)
                VStack(alignment: .center) {
                    bot(botImage: botimagefile, PrepareState: PrepareState, computerChoice: computerChoice)
                    LifeState(leftText:"電腦血量",Health: computerHealth, LossHealth: computerLossHealth, lifebarColor: Color.orange)
                    Text("⚔️⚔️⚔️").font(.largeTitle)
                    LifeState(leftText:"玩家血量",Health: playerHealth, LossHealth: playerLossHealth, lifebarColor: Color.yellow)
                    Text("\(result)")
                        .font(.title2)
                        .padding()
                    HStack {
                        Button(action: {
                            if !PrepareState {
                                self.playerChoice = "剪刀"
                                self.playGame()
                            }
                        }) {
                            Text(剪刀)
                                .font(.largeTitle).padding()
                                .background( Color.blue.opacity(PrepareState&&playerChoice=="剪刀" ? 1: 0.3))
                                .foregroundColor(.white)
                                .cornerRadius(10)
                        }
                        
                        Button(action: {
                            if !PrepareState {
                                self.playerChoice = "石頭"
                                self.playGame()
                            }
                        }) {
                            Text(石頭)
                                .font(.largeTitle).padding()
                                .background( Color.green.opacity(PrepareState&&playerChoice=="石頭" ? 1: 0.3))
                                .foregroundColor(.white)
                                .cornerRadius(10)
                        }
                        
                        Button(action: {
                            if !PrepareState {
                                self.playerChoice = "布"
                                self.playGame()
                            }
                        }) {
                            Text(布)
                                .font(.largeTitle).padding()
                                .background( Color.red.opacity(PrepareState&&playerChoice=="布" ? 1: 0.3))
                                .foregroundColor(.white)
                                .cornerRadius(10)
                            
                        }
                    }       
                    .alert((winner.isEmpty ? "請選擇下場的規則": "遊戲結束\n「\(winner)」獲勝！\n請選擇下場的規則"), isPresented: Binding(
                        get: { self.isGameEndedAndNotPrepare },
                        set: { _ in }
                    ), actions: {
                        Button("三戰兩勝") {
                            resetGame(resetMode: 0)
                        }
                        Button("五戰三勝") {
                            resetGame(resetMode: 1)
                        }
                        Button("七戰四勝") {
                            resetGame(resetMode: 2)
                        }
                    })
                }
                
            }
            
        }
        .background(LinearGradient(
            gradient: Gradient(colors: [Color.teal,Color.purple, Color.teal]),
            startPoint: .leading,
            endPoint: .trailing
        ))
    }
    // 其他函數
    func resetGame(resetMode: Int) {
        
        // 重置遊戲狀態，包括血量、結果等
        if(resetMode==0){
            computerHealth = "❤️❤️"
            playerHealth = "❤️❤️"
        }
        if(resetMode==1){
            computerHealth = "❤️❤️❤️"
            playerHealth = "❤️❤️❤️"
        }
        if(resetMode==2){
            computerHealth = "❤️❤️❤️❤️"
            playerHealth = "❤️❤️❤️❤️"
        }
        
        playerLossHealth = ""
        computerChoice=""
        
        computerLossHealth = ""
        result = ""
        isGameEnded = false
        winner = ""
        result="請選擇一個"
    }
    
    func reduceComputerHealth() {
        if computerHealth.count > 1 {
            computerHealth = String(computerHealth.prefix(computerHealth.count - 1))
            
        }else{
            computerHealth=""    
        }
        computerLossHealth+="❌"
    }
    func reducePleyerHealth() {
        if playerHealth.count > 1 {
            playerHealth = String(playerHealth.prefix(playerHealth.count - 1))
            
        }else{
             playerHealth=""
        }
        playerLossHealth+="❌"
    }
    func playGame() {
        let choices = ["剪刀", "石頭", "布"]
        let randomIndex = Int.random(in: 0..<choices.count)
        computerChoice = choices[randomIndex]

        if playerChoice == computerChoice {
            result = "平局"
            

        } else if (playerChoice == "剪刀" && computerChoice == "布") ||
                    (playerChoice == "石頭" && computerChoice == "剪刀") ||
                    (playerChoice == "布" && computerChoice == "石頭") {
            result = "你贏了！"
            reduceComputerHealth()
            botimagefile=win

        } else {
            result = "電腦贏了。"
             reducePleyerHealth()
             botimagefile=loss
        }
        if playerHealth.isEmpty {
            winner = "電腦"
            isGameEnded = true
        } else if computerHealth.isEmpty {
            winner = "玩家"
            isGameEnded = true
        }
        PrepareState = true // 設置為true以準備清空內容
        Timer.scheduledTimer(withTimeInterval: 2, repeats: false) { _ in
            PrepareState = false // 三秒後清空內容
            self.botimagefile=self.standby
            result="請選擇一個"
        }
    }
}



struct ContentView: View {
    var body: some View {
        PlayView()
    }
}


```
