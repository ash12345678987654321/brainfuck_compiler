brainfuck="++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>.>---.+++++++..+++.>>.<-.<.+++.------.--------.>>+.>++."
cells=[0]
loop=[0]
loop_pos=[]
cell_pos=0
lowest_cell=0
loop_s=0
n=0
counter=0
brainfuck=list(brainfuck)
for m in range(0,len(brainfuck)):
  s=brainfuck[m]
  if s=="[":
    counter+=1
  elif s=="]":
    counter-=1
  loop.append(counter)
if min(loop)<0:
  print ("Use a '[' before a ']'")
elif counter!=0:
  print ("Use the same number of '[' and ']'")
else:
  for m in range(0,len(loop)-1):
    a=loop[m]
    b=loop[m+1]
    if b==a+1:
      find=a
      find_pos=m+2
      boolean=True
      while boolean:
        if loop[find_pos]==a:
          boolean=False
          loop_pos.append([m,find_pos-1])
        else:
          find_pos+=1
  while n<len(brainfuck):
    s=brainfuck[n]
    if s=="+":
      cells[cell_pos-lowest_cell]+=1
    elif s=="-":
      cells[cell_pos-lowest_cell]-=1
    elif s=="<":
      if cell_pos==lowest_cell:
        cell_pos-=1
        lowest_cell-=1
        cells=[0]+cells
      else:
        cell_pos-=1
    elif s==">":
      cell_pos+=1
      if len(cells)<cell_pos-lowest_cell+1:
        cells.append(0)
    elif s==".":
      if 0<=cells[cell_pos-lowest_cell]<=1114111:
        print (chr(cells[cell_pos-lowest_cell]))
    elif s==",":
      num=int(ord(input("Input:")))
      cells[cell_pos-lowest_cell]=num
    elif s=="[":
      if cells[cell_pos-lowest_cell]==0:
        for i in range(len(loop_pos)):
          if loop_pos[i][0]==n:
            n+=loop_pos[i][1]-loop_pos[i][0]-1
    elif s=="]":
      if cells[cell_pos-lowest_cell]!=0:
        for i in range(len(loop_pos)):
          if loop_pos[i][1]==n:
            n-=loop_pos[i][1]-loop_pos[i][0]
    n+=1
