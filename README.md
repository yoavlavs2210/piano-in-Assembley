# piano-in-Assembley
A piano with a lot of variations and options in Assembly X86
data segment
    color db 0 
    color1 db 0  
    msg db "instructions:" ,0Dh, 0Ah, 24h
    msg1 db "press 1 to hear jingle bells" ,0Dh, 0Ah, 24h
    msg2 db "press 2 to hear hatikva" ,0Dh, 0Ah, 24h
    msg3 db "press 3 to hear what you have played" ,0Dh, 0Ah, 24h
    msg4 db "when you play a new song it will be     recorded automatically" ,0Dh, 0Ah, 24h
    msg5 db "press q to change the piano color" ,0Dh, 0Ah, 24h
    msg6 db "changing the white keys color" ,0Dh, 0Ah, 24h
    msg7 db "press 1 for blue" ,0Dh, 0Ah, 24h
    msg8 db "press 2 for red" ,0Dh, 0Ah, 24h
    msg9 db "press 3 for green" ,0Dh, 0Ah, 24h
    msg10 db "press 4 for yellow" ,0Dh, 0Ah, 24h
    msg11 db "press 5 brown" ,0Dh, 0Ah, 24h
    msg12 db "changing the black keys color" ,0Dh, 0Ah, 24h
    msg13 db "press w to change the piano color back" ,0Dh, 0Ah, 24h
    msg14 db "press a for help" ,0Dh, 0Ah, 24h 
    msg15 db "welcome to piano!" ,0Dh, 0Ah, 24h
    msg16 db "press any button to proceed" ,0Dh, 0Ah, 24h
    msg17 db "X - low do" ,0Dh, 0Ah, 24h
    msg18 db "E - high do" ,0Dh, 0Ah, 24h
    white db 15        ;move color white
    red db 4           ;move color red
    blue db 9
    gray db 8
    black db 0
    purple db 13
    green db 2
    yellow db 14
    brown db 6
    temp1 dw 0
    temp2 db 0
    temp3 db 0 
    temp4 dw 0
    temp5 db 0  
    temp6 db 0
    arr dw 100 dup (0) 
    len dw 0
    c db 0
    cnt db 0
    a db 2     
    
ends

stack segment
    dw   128  dup(0)
ends

code segment
    
               ; part 1: massege proc
    proc help  ; this proc contains the manual for the piano
        
        pusha
        mov ah, 00
        mov al, 02
        int 10h
        mov ax, 13h         ;transfers to grafic mode
        int 10h
        mov dx, offset msg17
        mov ah, 09
        int 21h
        mov dx, offset msg18
        mov ah, 09
        int 21h
        mov dx, offset msg
        mov ah, 09
        int 21h
        mov dx, offset msg1
        mov ah, 09
        int 21h
        mov dx, offset msg2
        mov ah, 09
        int 21h            
        mov dx, offset msg3
        mov ah, 09
        int 21h
        mov dx, offset msg4
        mov ah, 09
        int 21h
        mov dx, offset msg5
        mov ah, 09
        int 21h
        mov dx, offset msg13
        mov ah, 09
        int 21h
        mov dx, offset msg16
        mov ah, 09
        int 21h
        mov ah, 7h
        int 21h 
        mov ah, 00
        mov al, 02
        int 10h
        mov ax, 13h         ;transfers to grafic mode
        int 10h 
        mov dx, offset msg14
        mov ah, 09
        int 21h
        popa
    ret
    endp
     
         
                ; part 2: painting and graphic procs
     proc paint ; this proc draws a piano white key
        
     pusha
     cmp si, 30
     jz t
     cmp si, 81
     jz t
     cmp si, 151
     jz t
     cmp si, 201
     jz t   
       
     mov al, temp2
     cmp si, 100 
     jnz x1
x3:
     add si, 3
     jmp x2
x1:
     cmp si, 220 
     jz x3
     cmp si, 170 
     jz x3
     add si, 2     
x2:
     mov cx, si            ;tzir x mi
     mov di, si
     add di, 7
     mov dx, 81            ;tzir y mi
     jmp paint_2
     
     paint_1:
        
        inc dx            
        mov cx,si
     paint_2:
        mov ah,0ch
        mov bh,0h
        sub cx, 7
        int 10h  
        add cx, 7
        inc cx 
        cmp cx,di
        jnz paint_2
        cmp dx,110
        jnz paint_1
     
     cmp si, 103
     jz y2
     cmp si, 223
     jz y2
     cmp si, 173
     jz y2
     sub si, 2
     jmp y1
y2:     
     sub si, 3
y1:     
     
t:     
     mov al, temp2
     mov cx, si            ;tzir x mi
     mov di, si
     add di, 10
     mov dx, 50            ;tzir y mi
     jmp paint_a
     
     paint_b:
        
        inc dx            
        mov cx,si
     paint_a:
        mov ah,0ch
        mov bh,0h
        int 10h
        inc cx 
        cmp cx,di
        jnz paint_a
        cmp dx, 80
        jnz paint_b
        
     add di, 10   
        
     paint_d:
        
        inc dx 
        mov cx,si
     paint_c:
        mov ah,0ch
        mov bh,0h
        int 10h
        inc cx 
        cmp cx,di
        jnz paint_c
        cmp dx,110
        jnz paint_d
     
     inc cx
     mov si ,cx
     add di, 7
     mov dx, 80
     mov al, temp3   
        
     paint_e:
        
        inc dx 
        mov cx,si
     paint_f:
        mov ah,0ch
        mov bh,0h
        sub cx,7
        int 10h
        add cx,7
        inc cx 
        cmp cx,di
        jnz paint_f
        cmp dx,110
        jnz paint_e
        
      sub cx, 7     
      
      call grayline
      popa
      
      ret 
      endp
    
    
    proc paintd ; this proc draws a piano black key
        
     pusha
     mov al, temp2
     mov cx, si          ;tzir x 
     mov di, si
     add di, 10
     mov dx, 50          ;tzir y 
     jmp paint_ad
     
     paint_bd:
        
        inc dx            
        mov cx,si
     paint_ad:
        mov ah,0ch
        mov bh,0h
        int 10h
        inc cx 
        cmp cx,di
        jnz paint_ad
        cmp dx,80
        jnz paint_bd
        popa
        
        ret  
        endp
    
    
    proc paint1 ; ; this proc also draws a piano white key
        
        
     pusha
     mov al, temp2
     cmp si, 271 
     jz r
     add si, 2     
     mov cx, si            ;tzir x mi
     mov di, si
     add di, 7
     mov dx, 81            ;tzir y mi
     jmp paint_4
     
     paint_3:
        
        inc dx            
        mov cx,si
     paint_4:
        mov ah,0ch
        mov bh,0h
        sub cx, 7
        int 10h  
        add cx, 7
        inc cx 
        cmp cx,di
        jnz paint_4
        cmp dx,110
        jnz paint_3
        
     sub si, 2   
           
r:        
     mov al, temp2
     mov cx, si            ;tzir x mi
     mov di, si
     add di, 10
     mov dx, 50            ;tzir y mi
     jmp paint1_a
     
     paint1_b:
        
        inc dx 
        mov cx,si           ;note mi
     paint1_a:
        mov ah,0ch
        mov bh,0h
        int 10h
        inc cx 
        cmp cx,di
        jnz paint1_a
        cmp dx,110
        jnz paint1_b
     
     cmp si, 271
     jz y   
        
     call grayline1          ;making a red line
     
y:     
     popa
     ret   
     endp      
                  
    
    proc grayline ; this proc paints a grayline
     
     pusha
     inc cx         ;tzir x line
     mov dx, 81     ;tzir y do
     mov al, gray
     mov si, cx
     mov di, cx
     inc si
     jmp line_a
     
     line_b:
        
        inc dx             ;line
        mov cx,di
     line_a:
        mov ah,0ch
        mov bh,0h 
        sub cx,7
        int 10h
        add cx,7
        inc cx 
        cmp cx, si
        jnz line_a
        cmp dx, 110
        jnz line_b
        mov al, temp2
      
     popa   
     ret
     endp
     
     
     
     
     proc grayline1  ; this proc paints a grayline
     
     pusha
     inc cx         ;tzir x line
     mov dx, 50     ;tzir y do
     mov al, gray
     mov si, cx
     
     dec cx
     mov di, cx
     jmp line_a1
     
     line_b1:
        
        inc dx             ;line
        mov cx,di
     line_a1:
        mov ah,0ch
        mov bh,0h 
        int 10h
        inc cx 
        cmp cx, si
        jnz line_a1
        cmp dx, 110
        jnz line_b1
        mov al, temp2
        
     popa
     ret     
     endp   
        
        
                
    proc piano_w           ;the proc paints the piano with 2 octaves in white, its devided by piano characters.
        
     
     pusha
     mov temp2, bh
     mov temp3, bl
     
     mov si, 30          
     call paint            ; do
     
       
     mov si, 50             ; re   
     call paint          
           
   
     mov si, 70            ; mi
     call paint1
             
     
     mov si, 81             ; fa
     call paint
         
     
     mov si, 100              ; sol
     call paint       
            
        
     mov si, 120              ; la
     call paint 
         
         
     mov si, 140              ; see
     call paint1
       
        
     mov si, 151             ; high do
     call paint
            
          
     mov si, 170             ; high re        
     call paint 
            
        
     mov si, 190             ; high mi
     call paint1
            
     
     mov si, 201             ; high fa
     call paint
            
         
     mov si, 220             ; high sol
     call paint
               
            
     mov si, 240             ; high la
     call paint       
         
     mov si, 260             ; high see
     call paint1     
        
     mov si, 271             ; high high do
     call paint1
     popa
        
        ret
        endp
        
            
            
    proc piano_b   ;the proc paints the black keys in the piano, 2 octaves, its devided by piano characters.
        
     pusha
     mov temp2, bl 
        
     mov si, 40              ; do#
     call paintd       
            
     
     mov si, 60              ; re#
     call paintd       
     
     
     mov si, 90              ; fa#
     call paintd
     
     
     mov si, 110             ; sol#
     call paintd
     
     mov si, 130             ; la#
     call paintd
     
     
     mov si, 160             ; high do#
     call paintd
     
     
     mov si, 180             ; high re#
     call paintd
     
     
     mov si, 210             ; high fa#
     call paintd
     
     
     mov si, 230             ; high sol#
     call paintd
     
     mov si, 250             ; high la#
     call paintd
     
     popa
     ret  
    endp

    
     proc change_color ; this proc changes the color of the piano
            
            pusha
            mov len, 0
            mov cnt, 0
            mov ah, 00
            mov al, 02
            int 10h
            mov ax, 13h         ;transfers to grafic mode
            int 10h
            mov dx, offset msg
            mov ah, 09
            int 21h
            mov dx, offset msg6
            mov ah, 09
            int 21h
            mov dx, offset msg7
            mov ah, 09
            int 21h            
            mov dx, offset msg8
            mov ah, 09
            int 21h
            mov dx, offset msg9
            mov ah, 09
            int 21h
            mov dx, offset msg10
            mov ah, 09
            int 21h 
            mov dx, offset msg11
            mov ah, 09
            int 21h
            
z:                        
            mov ah, 7h
            int 21h
            cmp al, '1'
            jz p_blue
            cmp al, '2'
            jz p_red2
            cmp al, '3'
            jz p_green
            cmp al, '4'
            jz p_yellow
            cmp al, '5'
            jz p_brown
            jmp z

            
p_blue:
            mov bl, blue
            mov color, bl
            jmp z1
p_red2:      
            mov bl, red
            mov color, bl
            jmp z1       
p_green:
            mov bl, green
            mov color, bl
            jmp z1       
p_yellow:
            mov bl, yellow
            mov color, bl
            jmp z1        
p_brown:
            mov bl, brown
            mov color, bl
            jmp z1
            
p1_blue:
            mov bl, blue
            mov color1, bl
            jmp z2
p1_red2:      
            mov bl, red
            mov color1, bl
            jmp z2       
p1_green:
            mov bl, green
            mov color1, bl
            jmp z2       
p1_yellow:
            mov bl, yellow
            mov color1, bl
            jmp z2        
p1_brown:
            mov bl, brown
            mov color1, bl
            jmp z2
            
z1:                   
            mov ah, 00
            mov al, 02
            int 10h
            mov ax, 13h         ;transfers to grafic mode
            int 10h
            mov dx, offset msg12
            mov ah, 09
            int 21h
            mov dx, offset msg7
            mov ah, 09
            int 21h            
            mov dx, offset msg8
            mov ah, 09
            int 21h
            mov dx, offset msg9
            mov ah, 09
            int 21h
            mov dx, offset msg10
            mov ah, 09
            int 21h 
            mov dx, offset msg11
            mov ah, 09
            int 21h                   
            mov ah, 7h
            int 21h
            cmp al, '1'
            jz p1_blue
            cmp al, '2'
            jz p1_red2
            cmp al, '3'
            jz p1_green
            cmp al, '4'
            jz p1_yellow
            cmp al, '5'
            jz p1_brown
            jmp z1
z2:                    
            mov ah, 00
            mov al, 02
            int 10h
            mov ax, 13h         ;transfers to grafic mode
            int 10h
            mov bl, color
            mov bh, color
            call piano_w
            mov bl, color1
            call piano_b
            mov c, 1
            popa
            ret                                                                           
            endp
    
    
    proc bnl ;this proc changes the piano's color back to black and white
        
        pusha
        mov bl, white
        mov bh, white
        call piano_w
        mov bl, white
        mov color, bl
        mov bl, black
        mov color1, bl
        call piano_b 
        mov c, 1
        call st
        popa
        ret
                
    endp 
   
        

  
   
    proc play_note ;this proc saves in memory what you have played
        mov bp, sp 
        pusha
        mov dx, [bp + 2]
        mov si, offset arr
        mov bx, len
        shl bx, 1
        mov [si + bx], dx
        inc len    
        call play
        mov c, 0
        
        popa
        
        mov a, 2
        ret 2 
            
    endp
                       ;part 3: saving in memory procs
    proc read_from_mem ;this proc playes what you have played
        pusha 
        mov si, offset arr
        mov cx, len 
     play_notes:
        mov dx, [si]
        call play
        add si, 2  
        dec cnt
        cmp cnt, 0
        jz en 
        
        loop play_notes 
en:
        popa
  endp
            
                
                
               ; part 4: making sounds procs 
    proc play  ; this proc makes the sounds and pants the key 
     pusha   
            push dx
            mov bh, purple
            mov temp2, bh
            mov bh, 2
s:            
            cmp dx, 9121
            jz p_do
            cmp dx, 8609
            jz p_dod
            cmp dx, 8126
            jz p_re
            cmp dx, 7670
            jz p_red
            cmp dx, 7239
            jz p_mi
            cmp dx, 6833
            jz p_fa
            cmp dx, 6449
            jz p_fad
            cmp dx, 6087
            jz p_sol
            cmp dx, 5746
            jz p_sold
            cmp dx, 5423
            jz p_la
            cmp dx, 5119
            jz p_lad
            cmp dx, 4831
            jz p_see
            
            cmp dx, 4560
            jz p_hdo
            cmp dx, 4304
            jz p_hdod
            cmp dx, 4063
            jz p_hre
            cmp dx, 3834
            jz p_hred
            cmp dx, 3619
            jz p_hmi
            cmp dx, 3416
            jz p_hfa
            cmp dx, 3224
            jz p_hfad
            cmp dx, 3043
            jz p_hsol
            cmp dx, 2873
            jz p_hsold
            cmp dx, 2711
            jz p_hla
            cmp dx, 2559
            jz p_hlad
            cmp dx, 2415
            jz p_hsee
            cmp dx, 2280
            jz p_hhdo
            jmp s
            
            
        p_do:
            mov si, 30
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5 
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_dod:
            mov si, 40
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_re:
            mov si, 50
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_red: 
            mov si, 60
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_mi:
            mov si, 70
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint1
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_fa:
            mov si, 81
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_fad: 
            mov si, 90
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m    
                                 
        p_sol: 
            mov si, 100
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_sold: 
            mov si, 110
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_la: 
            mov si, 120
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_lad: 
            mov si, 130
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_see: 
            mov si, 140
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint1
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_hdo:
            mov si, 151
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hdod:
            mov si, 160
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hre:
            mov si, 170
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hred: 
            mov si, 180
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hmi:
            mov si, 190
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint1
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        p_hfa:
            mov si, 201
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_hfad: 
            mov si, 210
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m    
                                 
        p_hsol: 
            mov si, 220
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_hsold: 
            mov si, 230
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hla: 
            mov si, 240
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hlad: 
            mov si, 250
            mov temp5, bh
            mov bh, color1
            mov temp3, bh
            mov bh, temp5
            call paintd
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
            
        p_hsee: 
            mov si, 260
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint1
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m
        
        p_hhdo:
            mov si, 271
            mov temp5, bh
            mov bh, color
            mov temp3, bh
            mov bh, temp5
            call paint1
            mov temp5, bh
            mov bh, temp3
            mov temp2, bh
            mov bh, temp5
            dec bl
            cmp bl, 0
            jz k
            jmp m                            
        
  m:
        pop dx
        
        mov     al, 182         
        out     43h, al       
        mov     ax, dx       
                               
        out     42h, al        
        mov     al, ah         
        out     42h, al 
        in      al, 61h        
                               
        or      al, 00000011b   
        out     61h, al         
        mov     bx, 25          
pause1:
        mov     cx, temp4
pause2:
        dec     cx
        jne     pause2
        dec     bx
        jne     pause1
        in      al, 61h         
                               
        and     al, 11111100b  
        out     61h, al


        mov     al, 182         
        out     43h, al       
        mov     ax, dx       
                               
        out     42h, al        
        mov     al, ah         
        out     42h, al 
      
        mov     bx, 25          
pause3:
        mov     cx, 4000
pause4:
        dec     cx
        jne     pause4
        dec     bx
        jne     pause3
        

        mov bl, 1
        jmp s
        
        k: 
        
        popa   
        
        ret
        endp
        
        
    proc play1 ; this proc makes a break between sounds
        
        mov     al, 182         
        out     43h, al       
        mov     ax, dx       
                               
        out     42h, al        
        mov     al, ah         
        out     42h, al 
      
        mov     bx, 25          
pause5:
        mov     cx, 20000
pause6:
        dec     cx
        jne     pause6
        dec     bx
        jne     pause5 
        
        ret    
    endp             
    
    
       
    proc hatikva   ; this proc plays hatikva
        
        pusha
        mov bl, blue
        call piano_b
        mov bl, white
        mov bh, white
        call piano_w
        mov bl, white
        mov color, bl
        mov bl, black
        mov color1, bl
       
        mov dx, 5423
            
            call play
        
        mov dx, 4831
            
            call play
        
        mov dx, 4560
            
            call play
        
        mov dx, 4063
            
            call play
        
        mov dx, 3619
            
            call play
        
        mov dx, 3619
            
            call play
        
        mov dx, 3416
            
            call play
            
        mov dx, 3619
            
            call play
            
        mov dx, 3416
            
            call play
            
        mov dx, 2711
            
            call play
            
        mov dx, 3619
            
            call play
            
            call play1
        
        mov dx, 4063
            
            call play
        
        mov dx, 4063
            
            call play                                                             
        
        mov dx, 4063
            
            call play
            
        mov dx, 4560
            
            call play
            
        mov dx, 4560
            
            call play        
            
        mov dx, 4831
            
            call play
        
        mov dx, 5423
            
            call play
            
        mov dx, 4831
            
            call play
            
        mov dx, 4560
            
            call play
            
        mov dx, 5423
            
            call play
            
            call play1
            
        mov dx, 7239
            
            call play    
            
        mov dx, 5423
            
            call play
            
        mov dx, 4831
            
            call play
        
        mov dx, 4560
            
            call play
        
        mov dx, 4063
            
            call play
        
        mov dx, 3619
            
            call play
        
        mov dx, 3619
            
            call play
        
        mov dx, 3416
            
            call play
            
        mov dx, 3619
            
            call play
            
        mov dx, 3416
            
            call play
            
        mov dx, 2711
            
            call play
            
        mov dx, 3619
            
            call play     
        
            call play1
        
        mov dx, 4063
            
            call play
        
        mov dx, 4063
            
            call play                                                             
       
        mov dx, 4063
            
            call play
            
        mov dx, 4560
            
            call play
            
        mov dx, 4560     
            
            call play    
            
        mov dx, 4831
            
            call play
        
        mov dx, 5423
            
            call play
            
        mov dx, 4831
            
            call play
            
        mov dx, 4560
            
            call play
        
        mov dx, 5423
            
            call play
            
        mov dx, 7239
            
            call play
        
        mov dx, 5423
            
            call play           
        
        mov dx, 2711
            
            call play
            
        mov dx, 2711
            
            call play
        
        mov dx, 2711
            
            call play
        
        mov dx, 3043
            
            call play
        
        mov dx, 2711
            
            call play
        
        mov dx, 3043
            
            call play
            
        mov dx, 3416
            
            call play
        
        mov dx, 3619
            
            call play
            
            call play1
            
        mov dx, 5423
            
            call play           
        
        mov dx, 2711
            
            call play
            
        mov dx, 2711
            
            call play
        
        mov dx, 2711
            
            call play
        
        mov dx, 3043
            
            call play
            
        mov dx, 2711
            
            call play
        
        mov dx, 3043
            
            call play
            
        mov dx, 3416
            
            call play
        
        mov dx, 3619
            
            call play
            
        mov dx, 3043
            
            call play
            
        mov dx, 3043
            
            call play
           
        mov dx, 3043
            
            call play
            
        mov dx, 4560
            
            call play 
        
        mov dx, 4560
            
            call play
            
        mov dx, 4063
            
            call play                   
        
        mov dx, 3619
            
            call play    
                
        mov dx, 3416
            
            call play
          
        mov dx, 3043
            
            call play
             
        mov dx, 3619
            
            call play
             
        mov dx, 4063
            
            call play
             
        mov dx, 4560
            
            call play
              
        mov dx, 4063
            
            call play
             
        mov dx, 4063
            
            call play
              
        mov dx, 4560
            
            call play
               
        mov dx, 4560
            
            call play
              
        mov dx, 4831
            
            call play
               
        mov dx, 5423
            
            call play
            
        mov dx, 4831
            
            call play
              
        mov dx, 4560
            
            call play
                       
        mov dx, 5423
            
            call play
           
        mov dx, 4063
        
            call play    
            
        mov dx, 4063
            
            call play        
         
        mov dx, 4063
            
            call play    
            
        mov dx, 4560
            
            call play    
            
        mov dx, 4560
            
            call play    
         
        mov dx, 4063
            
            call play                       
           
        mov dx, 3619
            
            call play        
        
        mov dx, 3416
            
            call play    
          
        mov dx, 3043
            
            call play    
        
        mov dx, 3619
            
            call play    
            
        mov dx, 4063
            
            call play    
            
        mov dx, 4560
            
            call play    
            
        mov dx, 4063
            
            call play    
            
        mov dx, 4063
            
            call play    
            
        mov dx, 4560
            
            call play    
            
        mov dx, 4560
            
            call play    
            
        mov dx, 4831
            
            call play   
            
        mov dx, 5423
            
            call play    
          
        mov dx, 4831
            
            call play
            
        mov dx, 4560
        
            call play
            
         mov temp4, 60000
         
         mov dx, 5423
            
            call play                     
        
        popa
        ret
        endp
        

    proc jbl ; this proc plays jingle bells
        
        pusha
        mov bl, green
        call piano_b
        mov bl, red
        mov bh, red
        call piano_w
        mov bl, red
        mov color, bl
        mov bl, green
        mov color1, bl
        
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
        
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
        
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 3416
            call play
            
        mov dx, 3043
            call play
            
        mov dx, 2711
            call play
            call play1                
                     
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
        
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
                     
        mov dx, 3043
            call play
            
        mov dx, 3043
            call play
            
        mov dx, 2711
            call play
                     
        mov dx, 3043
            call play
            call play1
            
        mov dx, 2280
            call play
            call play1
             
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
        
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
        
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 3416
            call play
            
        mov dx, 3043
            call play
            
        mov dx, 2711
            call play
            call play1                
                     
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 2559
            call play
        
        mov dx, 2711
            call play
            
        mov dx, 2711
            call play
            call play1
            
        mov dx, 2711
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 2559
            call play
            
        mov dx, 3043
            call play                
            
        mov dx, 3416
            call play
            call play1
            
        mov dx, 4560
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 2280
            call play
            
        mov dx, 2559
            call play    
            
        mov dx, 3043
            call play
            
        mov dx, 3416
            call play
            
        mov bl, white
        mov color, bl
        mov bl, black
        mov color1, bl                                                            
                     
        popa
        ret
        endp
        
        
    proc st ; this proc is you play the piano

strt:        
    mov temp4, 40000
    mov ah, 7h
    int 21h
    
    cmp al, 'x'
    jz do
          
    cmp al, 'd'
    jz dod
          
    cmp al, 'c'
    jz re
    
    cmp al, 'f'
    jz red1
    
    cmp al, 'v'
    jz mi
    
    cmp al, 'b'
    jz fa
    
    cmp al, 'h'
    jz fad
    
    cmp al, 'n'
    jz sol
    
    cmp al, 'j'
    jz sold
      
    cmp al, 'm'
    jz la
    
    cmp al, 'k'
    jz lad
    
    cmp al, ','
    jz see
    
    cmp al, 'e'
    jz highdo
    
    cmp al, '4'
    jz highdod
         
    cmp al, 'r'
    jz highre 
    
    cmp al, '5'
    jz highred
    
    cmp al, 't'
    jz highmi
    
    cmp al, 'y'
    jz highfa 
    
    cmp al, '7'
    jz highfad
    
    cmp al, 'u'
    jz highsol
    
    cmp al, '8'
    jz highsold
    
    cmp al, 'i'
    jz highla
    
    cmp al, '9'
    jz highlad
    
    cmp al, 'o'
    jz highsee
    
    cmp al, 'p'
    jz highhdo
     
    cmp al, '1'
    jz mus1
    
    cmp al, '2'
    jz mus2
    
    cmp al, '3'
    jz mus3
    
    cmp al, 'q'
    jz cc      
    
    cmp al, 'w'
    jz pbnl
    
    cmp al, 'a'
    jz h
    jmp strt   
do: 

    mov dx, 9121    
    push dx
    inc cnt
    call play_note
    jmp strt
    
dod:

    mov dx, 8609
    push dx
    inc cnt
    call play_note
    jmp strt    
    
re:

    mov dx, 8126
    push dx 
    inc cnt
    call play_note
    jmp strt

red1:

    mov dx, 7670
    push dx  
    inc cnt
    call play_note
    jmp strt    

mi:
 
    mov dx, 7239                                                                                                                                                                                       
    push dx
    inc cnt
    call play_note
    jmp strt     
    
fa:
 
    mov dx, 6833
     push dx 
     inc cnt
     call play_note
    jmp strt
    
fad:

    mov dx, 6449
    push dx 
    inc cnt
    call play_note
    jmp strt    

sol:

    mov dx, 6087
    push dx
    inc cnt
    call play_note
    jmp strt

sold:

    mov dx, 5746
    push dx 
    inc cnt
    call play_note
    jmp strt    

la:
 
    mov dx, 5423
    push dx 
    inc cnt
    call play_note
    jmp strt

lad:

    mov dx, 5119
    push dx 
    inc cnt
    call play_note
    jmp strt    

see:

    mov dx, 4831
     push dx 
     inc cnt
    call play_note
    jmp strt
    
highdo:

    mov dx, 4560
    push dx
    inc cnt
    call play_note
    jmp strt
    
highdod:

    mov dx, 4304
    push dx
    inc cnt
    call play_note
    jmp strt
    
highre:

    mov dx, 4063
    push dx 
    inc cnt
    call play_note
    jmp strt    
    
highred:

    mov dx, 3834
    push dx 
    inc cnt
    call play_note
    jmp strt
    
highmi:

    mov dx, 3619
     push dx 
     inc cnt
     call play_note
    jmp strt    
    
highfa:

    mov dx, 3416
     push dx
     inc cnt
    call play_note
    jmp strt    
    
highfad:

    mov dx, 3224
    push dx 
    inc cnt
    call play_note
    jmp strt                            
            
highsol:

    mov dx, 3043
    push dx
    inc cnt
    call play_note
    jmp strt 
    
highsold:

    mov dx, 2873
    push dx 
    inc cnt
    call play_note
    jmp strt
    
highla:

    mov dx, 2711
     push dx
     inc cnt
    call play_note
    jmp strt
    
highlad:

    mov dx, 2559
    push dx
    inc cnt
    call play_note
    jmp strt
    
highsee:

    mov dx, 2415
    push dx
    inc cnt
    call play_note
    jmp strt
    
highhdo:

    mov dx, 2280
     push dx
     inc cnt
    call play_note
    jmp strt                        
  
    
mus1:
     call jbl
     mov bl, black
     call piano_b
     mov bl, white
     mov bh, white
     call piano_w
     mov c, 1 
     mov len, 0
     mov cnt, 0
     jmp strt
    
mus2:
    call hatikva
    mov bl, black
    call piano_b 
    mov c, 1
    mov len, 0
    mov cnt, 0
    jmp strt
    
mus3:
    mov bl,  cnt
    mov temp6, bl
    dec c
    cmp c, 0
    jz c1
    dec cnt
    call read_from_mem
    mov len, 0
    mov cnt, 0
    jmp c2
c1:
    inc c 
c2:   
    mov bl,  temp6
    mov cnt , bl
    jmp strt    
   
cc:
    call change_color
    mov dx, offset msg14
    mov ah, 09
    int 21h
    jmp strt  
    
pbnl:
    call bnl
    jmp strt
    
h:
    call help
    mov bl, color
    mov bh, color
    call piano_w
    mov bl, color1
    call piano_b
    jmp strt
  
  popa  
ret
endp
       
              
start:
    
    mov ax,data
    mov ds, ax
    mov ax, 13h         ;transfers to grafic mode
    int 10h
    mov dx, offset msg15
    mov ah, 09
    int 21h
    mov dx, offset msg16
    mov ah, 09
    int 21h
    mov ah, 7h
    int 21h 
    mov ah, 00
    mov al, 02
    int 10h
    mov ax, 13h         ;transfers to grafic mode
    int 10h
    call help          
    mov bl, white
    mov bh, white
    call piano_w
    mov bl, white
    mov color, bl
    mov bl, black
    mov color1, bl
    call st

mov ax, 4c00h
int 21h  

ends

end start
