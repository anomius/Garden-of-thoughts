---
title: "The iQuHack Blog"
tags:
- "experence"
- "full on memeing"
---

Made a game of life on Quantum Game Of life

!()[notes/images/ezgif-6-f0664836c1.gif]
is baar full flex baji kari learnt a lot in 3d rendering and voxel outputs 
!()[notes/images/output.gif]
```python
import numpy as np

# Importing standard Qiskit libraries

from qiskit import QuantumCircuit,QuantumRegister,ClassicalRegister,transpile, Aer, IBMQ, execute

from qiskit.quantum_info import Operator, Statevector

from qiskit.providers.aer import QasmSimulator,backends

backend = QasmSimulator()

from rich import print

from pyvox.models import Vox,Color

from pyvox.writer import VoxWriter

    

def get_life(nh):

 v=nh

 a=0

 for i in [0,2]:

 a+=(v[1][1][i]+v[i][1][1]+v[1][i][1])/2

 for i in [0,2]:

 a+=(v[0][i][0]+v[0][i][2]+v[2][i][0]+v[2][i][2])/8

 a+=(v[1][0][0]+v[1][2][2]+v[1][2][0]+v[1][0][2]+v[0][0][1]+v[0][1][0]+v[0][1][2]+v[0][2][1]+v[2][0][1]+v[2][1][0]+v[2][1][2]+v[2][2][1])/4

 return a

def get_board_vox(board,t):

 temp=(board/np.max(board))*255

 temp= temp.astype(int)

 v=Vox.from_dense(temp)

 x=f'test{t}.vox'

 VoxWriter(x, v).write()

 print(v)

def get_neboiurs(board,x,y,z):

 return board[x-1:x+2,y-1:y+2,z-1:z+2] 

def update_board(board):

 board_c=board.copy()

 for i in range(1,len(board_c)-1):

 for j in range(1,len(board_c[i])-1):

 for k in range(1,len(board_c[i][j])-1):

 board_c[i][j][k]=get_life(get_neboiurs(board,i,j,k))

 quantum(nh)

 return board_c

  

def quantum(nh):

 def diffuser(n):

 qc = QuantumCircuit(n,name='Diff')

 qc.h(range(n))

 qc.append(phase_oracle(n,[0]),range(n))

 qc.h(range(n))

 qc.draw()

 return qc

  

 # big ball of wibbly-wobbly, timey-wimey stuff

 def condenser(n,marked):

 qc = QuantumCircuit(n)

 print(f'{n} qubits, basis state {marked} marked')

 qc.h(range(n))

 qc.append(phase_oracle(n,marked),range(n))

 qc.append(diffuser(n),range(n))

 return qc

  

 value=nh[1][1][1]

 alive = np.array([1.0,0.0])

 dead = np.array([0.0,1.0])

 B = np.array([[0,0],[1,1]])

 D = np.array([[1,1],[0,0]])

 S = np.array([[1,0],[0,1]])

 a=get_life(nh)

 if a <= 1:

 value = dead

 elif (a > 1 and a <= 3):

 value = ((np.sqrt(2)+1)*2-(np.sqrt(2)+1)*a)*dead+(a-1)*value

 elif (a > 3 and a <= 4):

 value = (((np.sqrt(2)+1)*3)-(np.sqrt(2)+1)*a)*value+(a-2)*alive

 elif (a > 4 and a < 5):

 value = ((np.sqrt(2)+1)*4-(np.sqrt(2)+1)*a)*alive+(a-3)*dead

 elif a >= 5:

 value = dead

  

 value = value/np.linalg.norm(value)

 a=a/8

 a = a/np.linalg.norm(a)

 qr = QuantumRegister(5)

 cr = ClassicalRegister(5)

 qc = QuantumCircuit(qr, cr,name='Morpheous')

 qc.initialize([a,0],[qr[0]])

 qc.initialize(value,[qr[1]])

 qc.initialize(value,[qr[2]])

 qc.cx(qr[0],qr[2])

 qc.cx(qr[1],qr[3])

 qc.cx(qr[2],qr[4])

 qc.cx(qr[4],qr[1])

 qc.barrier()

 qc.append(condenser(5,[int(a)]),range(5)) #had some issues h

 qc.append(diffuser(5),range(5))

 qc.measure(range(n),range(n))

 print(qc.draw())

 back = Aer.get_backend('qasm_simulator')

 result = execute(qc,back,shots=2048).result()

 counts = result.get_counts(qc)

 print(counts)

  

 return counts

  
  

i=0

x,y,z=6,6,6

board=np.zeros((x,y,z))

board[1][1][1]=1

board[1][1][2]=1

board[1][1][3]=1

board[1][2][1]=1

board[1][2][2]=1

board[1][2][3]=1

get_board_vox(board,i)

while i<30:

 board=update_board(board)

 get_board_vox(board,i)

 print(board)

 i+=1

print(board)
```

baki ka baad mai likhunga 
## 🤌🏻👌🏻 Bye
