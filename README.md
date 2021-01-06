# AE-DMG-Calculator
#オンラインシングルRPGアナザーエデン時空を超える猫の物理攻撃ダメージ計算機の試作品です

import tkinter
from tkinter import messagebox

if __name__ == "__main__":
    root = tkinter.Tk()
    root.title("アナザーエデン 物理攻撃用砂袋計算機")
    root.geometry("360x500")

    #入力欄を設定
    input_box1 = tkinter.Entry(width=40)
    input_box1.place(x=10, y=35)
    input_box2 = tkinter.Entry(width=40)
    input_box2.place(x=10, y=80)
    input_box3 = tkinter.Entry(width=40)
    input_box3.place(x=10, y=125)
    input_box4 = tkinter.Entry(width=40)
    input_box4.place(x=10, y=170)
    input_box5 = tkinter.Entry(width=40)
    input_box5.place(x=10, y=215)
    input_box6 = tkinter.Entry(width=40)
    input_box6.place(x=10, y=260)
    input_box7 = tkinter.Entry(width=40)
    input_box7.place(x=10, y=305)
    input_box8 = tkinter.Entry(width=40)
    input_box8.place(x=10, y=350)
    input_box9 = tkinter.Entry(width=40)
    input_box9.place(x=10, y=395)
    input_box10 = tkinter.Entry(width=40)
    input_box10.place(x=10, y=440)
    
    #入力欄に入れてほしい項目
    input_label1 = tkinter.Label(text="攻撃")
    input_label1.place(x=10, y=10)
    input_label2 = tkinter.Label(text="腕力")
    input_label2.place(x=10, y=55)
    input_label3 = tkinter.Label(text="守備値")
    input_label3.place(x=10, y=100)
    input_label4 = tkinter.Label(text="魔力")
    input_label4.place(x=10, y=145)
    input_label5 = tkinter.Label(text="スキル倍率")
    input_label5.place(x=10, y=190)
    input_label6 = tkinter.Label(text="その他の上昇率")
    input_label6.place(x=10, y=235)
    input_label7 = tkinter.Label(text="クリティカル（有か無を入力）")
    input_label7.place(x=10, y=280)
    input_label8 = tkinter.Label(text="弱点（有か無を入力）")
    input_label8.place(x=10, y=325)
    input_label9 = tkinter.Label(text="耐性（有か無を入力）")
    input_label9.place(x=10, y=370)
    input_label10 = tkinter.Label(text="攻撃属性（属性攻撃か無属性攻撃を入力）")
    input_label10.place(x=10, y=415)
    
    #入力後、測定ボタンを押した後の挙動
    def button_click(): 
        input_value1 = input_box1.get()    #攻撃力(バフ・デバフはここに乗る)
        input_value2 = input_box2.get()    #腕力
        input_value3 = input_box3.get()    #敵の防御値(敵のバフ・デバフはここで)
        input_value4 = input_box4.get()    #魔力
        input_value5 = input_box5.get()    #スキル倍率
        input_value6 = input_box6.get()    #武器やグラスタ(特殊装備)、状態異常時威力増加、クリダメupによる上昇率(無い場合は１)
        input_value7 = input_box7.get()    #クリティカルの有無(1が発生、0がクリティカル無)
        input_value8 = input_box8.get()    #弱点の有無(1が弱点、0が非弱点)
        input_value9 = input_box9.get()    #耐性の有無(1が耐性有、0が耐性無)
        input_value10 = input_box10.get()  #属性の有無(1が属性、0が無属性)
        
        def SandBag_P():    #ダメージ計算を行う関数
            import random as rn
            import math        
            
            #input_boxで得た値(input_value)を変数として利用
            A = int(input_value1)
            B = int(input_value2)
            C = int(input_value3)
            D = int(input_value4)
            P = float(input_value5)
            W = float(input_value6)
            while True:     #得られた特定のstring型の文字を数値変換して式に組み込むための儀式
                Crt = str(input_value7)
                if Crt == "有":
                    Crt == 1
                    break
                elif Crt == "無":
                    Crt== 0
                    break
                else:
                    print("有か無を入力")
                    
            while True:
                Weak = str(input_value8)
                if Weak == "有":
                    Weak == 1
                    break
                elif Weak == "無":
                    Weak == 0
                    break
                else:
                    print("有か無を入力")
            
            while True:
                Resist = str(input_value9)
                if Resist == "有":
                    Resist == 1
                    break
                elif Resist == "無":
                    Resist== 0
                    break
                else:
                    print("有か無を入力")
                    
            while True:
                At = str(input_value10)
                if At == "属性攻撃":
                    At == 1
                    break
                elif At == "無属性攻撃":
                    At== 0
                    break
                else:
                    print("属性攻撃か無属性攻撃を入力")
            
            #クリティカル発生時と無発生時、また属性の有無などの条件の違いで用いられる式が若干異なるので、予めここで定義
            E = D*10+16
            El = math.sqrt(E)
            r = rn.randint(16,47)
            R = A*r/25.6
            X = (((A-(C/4))*((B/32)+1)*3.25*(((El-4)/64)+1) + R))*P*W
            x = (((A-(C/4))*((B/32)+1)*3.25 + R))*P*W
            Y = (((A-(C/2))*((B/32)+1)*1.75*(((El-4)/64)+1) + R))*P*W
            y = (((A-(C/2))*((B/32)+1)))*1.75*P*W
            Z = X
            Z = Y
            Z = x
            Z = y
            
            if At == 1:     #属性の有無の条件分岐(この場合は属性攻撃の時)
                if Crt == 1:        #クリティカルの有無の条件分岐
                    if Weak == 1:   #攻撃属性が弱点の時の条件分岐
                        Z = X*((D+ math.sqrt(D*2))/512+1.85)
                    elif Weak == 1 and Resist == 1:     #属性は弱点かつ攻撃種(斬・突・打)に耐性を持つ場合の条件分岐
                        Z = X*(((D+ math.sqrt(D*2))/512+1.85)-0.25)
                    elif Weak == 0:     #攻撃属性が弱点属性ではない場合
                        if Resist == 0:     #攻撃種に耐性を持つ場合
                            Z = X*1
                        elif Resist == 1:       #攻撃種に耐性を持たない場合
                            Z = X*0.25
                            
                elif Crt == 0:
                    if Weak == 1:
                        Z = Y*((D+ math.sqrt(D*2))/512+1.85)
                    elif Weak == 1 and Resist == 1:
                        Z = Y*(((D+ math.sqrt(D*2))/512+1.85)-0.25)
                    elif Weak == 0:
                        if Resist == 0:
                            Z = Y*1
                        elif Resist == 1:
                            Z = Y*0.25
                            
            elif At == 0:
                if Crt == 1:
                    if Weak == 1:
                        Z = x*((D+ math.sqrt(D*2))/512+1.85)
                    elif Weak == 1 and Resist == 1:
                        Z = x*(((D+ math.sqrt(D*2))/512+1.85)-0.25)
                    elif Weak == 0:
                        if Resist == 0:
                            Z = x*1
                        elif Resist == 1:
                            Z = x*0.25
                            
                elif Crt == 0:
                    if Weak == 1:
                        Z = y*((D+ math.sqrt(D*2))/512+1.85)
                    elif Weak == 1 and Resist == 1:
                        Z = y*(((D+ math.sqrt(D*2))/512+1.85)-0.25)
                    elif Weak == 0:
                        if Resist == 0:
                            Z = y*1
                        elif Resist == 1:
                            Z = y*0.25
                            
            print(int(Z))
            return int(Z)
            
        value = SandBag_P()     #関数SandBag_P()で得られた値を取得
        messagebox.showinfo("予測結果",value)    #結果を別ウィンドウに表示
    
    def close_window():     #ウィンドウを消すための関数
        root.destroy()
    
    #ボタンの設定
    button = tkinter.Button(text="予測",command=button_click) #ボタンを押した時に、先程の関数button_clickを起動
    button.place(x=10, y=465)
    button = tkinter.Button(text="終了",command=close_window) #ボタンを押したときにウィンドウを閉じる
    button.place(x=50, y=465)
    
    root.mainloop()
