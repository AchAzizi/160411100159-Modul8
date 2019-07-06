# Rangkuman-Modul8
# Tree dan Binary Tree

Tree merupakan struktur data yang berbentuk non linear, berbeda dengan struktur data stack, queue, ataupun deque.
Bentuk Tree di computer science hampir sama dengan tree yang terdapat pada ekosistem biologi,
yaitu keduanya memiliki root, leaves, dan branches.

# istilah-istilah umum dalam tree.
Node      :  merupakan bagian dari tree yang menyimpan informasi atau juga disebut sebagai key
Edge      : yang menghubungkan antara node yang satu dengan yang lain. 
            Hanya ada satu edge yang masuk ke dalam node, dan satu atau lebih edge yang keluar dari suatu node
Root      : node yang terletak di paling atas, tidak ada edge yang masuk ke dalam node root ini,
            tapi root mempunyai satu atau lebih dari satu edge yang keluar.
path      : merupakan urutan node dari root sampai tujuan, misalkan computer --> D: --> Mata Kuliah --> Struktur Data
children  : merupakan node-node yang memiliki edge yang masuk dari node yang sama. Misalkan program files, users,
            dan windows merupakan children, krn memiliki edge masuk yang sama-sama berasal dari node C:
Parent    : node yang memiliki edge yang keluar dari node tersebut, misalkan node C: adalah parent dari program files, users,
            dan windows
Siblings  : adalah node-node yang berasal dari parent yang sama
subtree   : kumpulan dari node dan edge yang terdiri dari parent dan semua node setelah parent
leaf node : node yang tidak memiliki edge yang keluar, node yang tidak memiliki children
level     : tingkatan dari node. Root merupakan level ke-0, semakin kebawah maka level dari node tersebut semakin besar,
            misalkan struktur data berada di level ke-3
height    : merupakan tinggi tree, nilai dari height ini adalah level maksimum dari tree


# Binaary Tree dalam Struktur Data
Berikut implementasi class binary Tree, dimana pada class ini terdapat tiga buah property atau state,
yaitu key, leftChild, dan rightChild. Key digunakan untuk informasi nilai yang terdapat pada node, lefchild dan
rightchild digunakan sebagai pointer untuk menunjukkan child sebelah kiri dan kanan dari node

      class BinaryTree:
          def __init__(self, root):
              self.key = root
              self.leftChild = None
              self.rightChild = None
              
      myTree=BinaryTree(10)
      print(myTree.leftChild)
      
Pada class yang sudah dibuat tersebut, terdapat suatu constructor, yaitu node akan dibuat setiap sebuah object didefinisikan dengan
menggunakan tipe data class BinaryTree ini. 
Class BinaryTree ini harus memiliki dua method utama yaitu, insertLeft dan insertRight. Pada method insertLeft ini,
sebuah subtree akan dibuat, dan dilekatkan terhadap tree utama dari edge root yang sebelah kiri, begitu juga insertRight.

      class BinaryTree:
          def __init__(self, root):
              self.key = root
              self.leftChild = None
              self.rightChild = None
          def insertLeft(self, new_node):
              if self.leftChild == None:
                  self.leftChild = BinaryTree(new_node)
              else:
                  t = BinaryTree(new_node)
                  t.leftChild = self.leftChild
                  self.leftChild = t
          def insertRight(self, new_node):
              if self.rightChild == None:
                  self.rightChild = BinaryTree(new_node)            
              else:
                  t = BinaryTree(new_node)
                  t.rightChild = self.rightChild
                  self.rightChild = t
                  
Pada method insertLeft tersebut perlu dilakukan pemeriksaan terlebih dahulu,
apakah child kiri dari node yang akan disisipi subtree baru masih kosong, jika iya maka subtree tersebut dimasukkan pada leftChild.
Ilustrasi insertLeft pada suatu binary tree yang pointer leftchild masih kosong.
Misalkan tree 't' akan disisipkan pada tree 'a', dimana leftchild dari tree a, masih kosong, sehingga dapat langsung diperintahkan :

      self.leftChild=BinaryTree(new_node)

Jika penyisipan dilakukan pada suatu binary tree, dimana leftchild tree tersebut tidak kosong.
Misalkan terdapat tree 'a', dimana tree 'a' tersebut, memiliki leftchild, yaitu 'b'.
Jika ingin dilakukan penyisipan tree baru, yaitu 't', maka tahapan yang harus dilakukan adalah :

      1. t.leftChild = self.leftChild
      2. self.leftChild = t
      
Perintah pada baris pertama digunakan agar node yang terletak pada left child tetap ada dan tidak hilang.
Jika perintah tersebut dibalik menjadi :

      1. self.leftChild = t
      2. t.leftChild = self.leftChild
      
Maka node yang merupakan leftchild dari node utama akan hilang, karena tidak ada pointer yang menunjuk ke leftchild tersebut.

Berikut tambahan method pada class BinaryTree, untuk mendapatkan informasi mengenai left child, right child, dan
root dari suatu binary tree.

      class BinaryTree:
          def __init__(self, root):
              self.key = root
              self.leftChild = None
              self.rightChild = None
          def insertLeft(self, new_node):
              if self.leftChild == None:           
                  self.leftChild = BinaryTree(new_node)         
              else:
                  t = BinaryTree(new_node)
                  t.leftChild = self.leftChild
                  self.leftChild = t

          def insertRight(self, new_node):
              if self.rightChild == None:
                  self.rightChild = BinaryTree(new_node)            
              else:
                  t = BinaryTree(new_node)
                  t.rightChild = self.rightChild
                  self.rightChild = t

          def getRightChild(self):
              return self.rightChild
          def getLeftChild(self):
              return self.leftChild
          def setRootVal(self, obj):
              self.key = obj
          def getRootVal(self):
              return self.key
    
    
# Pharsing Binary Tree
Binary tree dapat digunakan untuk beberapa aplikasi seperti penyelesaian persamaan matematika.
Misalkan terdapat persamaan ((7+3)*(5-2))

Penyelesaian persamaan matematika tergantung pada operator precedence dan keberadaan kurung.
Jika terdapat tanda kurung buka maupun tutup, maka persamaan di dalam kurung tersebut haruslah diselesaikan pertama kali
walapun level operator precedence lebih rendah dibandingkan operator yang berada di luar kurung.

Terdapat dua tahapan untuk menyelesaikan Persamaan Matematikan tersebut, dengan menggunakan Binary Tree, yaitu :
  1. Pembentukan Parse Tree
  2. Evaluasi Persamaan Matematika

# Pembuatan Parse Tree untuk Ekspressi Matematika
Persamaan Matematika harus dipecah menjadi list token agar dapat dibuat menjadi parse tree.
Token-token untuk persamaan Matematika tersebut antara lain:
  1. Kurung buka, kurung buka ini menandakan ekspressi baru yang akan dioperasi, oleh karena itu perlu dibuat subtree
     baru untuk menyelesaikan ekspressi baru ini
  2. kurung tutup, kurung tutup ini menandakan akhir dari ekspressi matematika
  3. operand, operand ini yang akan jadi leaf node dan children dari operator
  4. operator, operator merupakan parent dan punya left maupun right child
  
  
Berikut algoritma untuk membuat parse tree ekspressi matematika:
  1. Jika current token adalah kurung buka, '(' , tambahkan node baru sebagai left child dari current Node dan jadikan node
     baru ini sebagai current node
  2. jika current token adalah operator, set nilai key dari current node dengan operator tersebut.
     Tambahkan node baru sebagai right child dari current node, jadikan right child ini sebagai current node
  3. jika current token adalah operand, maka set nilai key dari current node dengan operand tersebut dan jadikan parent
     dari node tersebut menjadi current node
  4.jika current token adalah kurung tutup, ')', maka kembali ke parent dari current node


Binary tree class sebelumnya menyediakan method-method untuk menambah node baru baik sebelah kiri maupun kanan,
dan menuju left child maupun right child. Method-method ini sangat diperlukan untuk pembuatan parse tree.
Berdasarkan algoritma pembuatan parse tree diatas, terdapat perintah untuk kembali menuju parent dari current node.
Hal ini tidak dapat dilakukan oleh method yang terdapat pada binary tree class sebelumnya.

          ///stack
          def stack():
              s=[]
              return (s)

          def push(s,data):
              s.append(data)

          def pop(s):
              data=s.pop()
              return(data)

          def peek(s):
              return(s[len(s)-1])

          def isEmpty(s):
              return (s==[])

          def size(s):
              return(len(s))

          ///class
          class BinaryTree:
              def __init__(self, root):
                  self.key = root
                  self.leftChild = None
                  self.rightChild = None
              def insertLeft(self, new_node):
                  if self.leftChild == None:           
                        self.leftChild = BinaryTree(new_node)         
                  else:
                        t = BinaryTree(new_node)
                        t.leftChild = self.leftChild
                        self.leftChild = t

              def insertRight(self, new_node):
                  if self.rightChild == None:
                        self.rightChild = BinaryTree(new_node)            
                  else:
                        t = BinaryTree(new_node)
                        t.rightChild = self.rightChild
                        self.rightChild = t

              def getRightChild(self):
                  return self.rightChild
              def getLeftChild(self):
                  return self.leftChild
              def setRootVal(self, obj):
                  self.key = obj
              def getRootVal(self):
                  return self.key

          ///ParseTree
          def buildParseTree(mathExp):
              tokenList = mathExp.split()
              parentStack = stack()
              expTree = BinaryTree(' ' )
              push(parentStack,expTree)
              print(tokenList)
              currentTree = expTree
              for i in tokenList:

                  if i == '(' :
                        print('if 1', i)
                        currentTree.insertLeft(' ' )
                        push(parentStack,currentTree)
                        currentTree = currentTree.getLeftChild()
                  elif i not in [ '+' , '-' , '*' , '/' , ')' ]:
                        print('if 2', i)
                        currentTree.setRootVal(int(i))

                        parent = pop(parentStack)
                        currentTree = parent
                  elif i in [ '+' , '-' , '*' , '/' ]:
                        print('if 3', i)
                        currentTree.setRootVal(i)
                        currentTree.insertRight(' ' )
                        push(parentStack,currentTree)
                        currentTree = currentTree.getRightChild()
                  elif i == ')' :

                        currentTree = pop(parentStack)
                  else:
                        raise ValueError
              return expTree

          ///Main
          pt = buildParseTree(' ( 3 + ( 4 * 5 ) ) ')

          >>>
          Running: ['(', '3', '+', '(', '4', '*', '5', ')', ')']
             if 1 (
             if 2 3
             if 3 +
             if 1 (
             if 2 4
             if 3 *
             if 2 5

          print(pt.getRootVal())
          tmp=pt.getLeftChild()
          print(tmp.getRootVal())
          
          +
          3

          if pt.getLeftChild():
            print('Tree')
            
          Tree
          

# Evaluasi Persamaan Matematika
Untuk menyelesaikan persamaan matematika dengan menggunakan binary tree, diperlukan penyelesaian terlebih dahulu secara rekursif
subtree dari binary tree tersebut. Untuk membuat fungsi rekursif, base case dari fungsi rekursif tersebut harus ditentukan
terlebih dahulu.

Base case untuk penyelesaian persamaan matematika dengan binary tree secara rekursif adalah pada saat berada di leaf node.
leaf node ini tidak memiliki child lagi sehingga, rekursif berhenti pada saat berada di posisi leaf node, dan informasi yang berada
di leaf node ini adalah informasi operand. Oleh karena itu nilai balik fungsi rekursif ketika berada di posisi leaf node adalah
informasi node itu sendiri (key).

Rekursif dilakukan dengan cara mengoperasikan left child dan right child dengan operator yang sesuai.
Hasil dari operasi ini kemudian digunakan sebagai nilai balik untuk operasi binary tree level diatasnya.

Berikut fungsi rekursif untuk mengevaluasi persamaan matematika dengan menggunakan binary tree:

      import operator
      def evaluate(parse_tree):
          opers = { '+' :operator.add, '-' :operator.sub, '*' :operator.mul,'/' :operator.truediv}
          left = parse_tree.getLeftChild()
          right = parse_tree.getRightChild()
          if left and right:
              fn = opers[parse_tree.key]
              return fn(evaluate(left),evaluate(right))
          else:
              return parse_tree.key

      evaluate(pt)
      
      23
  
  
# Soal PRaktikum
Buatlah fungsi untuk membangun sebuah binary tree (Gunakan class Binary Tree yang telah dibuat) yang merepresentasikan
operasi matematika postfix, seperti contoh berikut :
Operasi matematika : 2 8 9 + *, yang akan menghasilkan binary tree sebagai berikut :

Algoritma untuk membangun binary tree tersebut adalah :
1. Jika token adalah sebuah operand, maka :
    a. Buat tree, dengan node (root) adalah operand tersebut
    b. Masukkan tree ke dalam stack
2. Jika token adalah operator, maka :
    a. Pop dua buah tree teratas (misal B dan C)
    b. Buat tree baru (misal A) dengan root node adalah operator
    c. Set B menjadi right child dari A
    d. Set C menjadi left child dari A
    e. Push tree yang terbentuk ke dalam stack
    
Tambahkan fungsi evaluate yang sudah dibuat sebelumnya di dalam kelas (untuk mengoperasikan binary tree yang sudah dibangun).

Perintah untuk eksekusi :

      a='2 8 9 + *'
      resTree=buildTree(a)
      evaluate(resTree)
      
Contoh hasil eksekusi :

      a='2 8 9 + *'
      resTree=buildTree(a)
      evaluate(resTree)

      34

Contoh hasil eksekusi :

      a='2 4 + 3 5 * -'
      resTree=buildTree(a)
      evaluate(resTree)

      -9

      a='10 3 2 12 + - *'
      resTree=buildTree(a)
      evaluate(resTree)

      -110


# Jawaban Praktikum

      def main():
          pass
      if __name__ == '__main__':
          main()

      import operator
      class Stack:
           def __init__(self):
               self.items = []
           def isEmpty(self):
               return self.items == []
           def push(self, item):
               self.items.append(item)
           def pop(self):
               return self.items.pop()
           def peek(self):
               return self.items[len(self.items)-1]
           def size(self):
               return len(self.items)
      class BinaryTree:
          def __init__(self,rootObj):
              self.key = rootObj
              self.leftChild = None
              self.rightChild = None
          def insertLeft(self,newNode): #insertLeft untuk membuat Node baru kedalam insertLeft.
              if self.leftChild == None:
                  self.leftChild = BinaryTree(newNode)
              else:
                  t = BinaryTree(newNode)
                  t.leftChild = self.leftChild
                  self.leftChild = t
          def insertRight(self,newNode): #insertRight untuk membuat Node baru kedalam insertRight
              if self.rightChild == None:
                  self.rightChild = BinaryTree(newNode)
              else:
                  t = BinaryTree(newNode)
                  t.rightChild = self.rightChild
                  self.rightChild = t      
          def getRightChild(self): #GetRightChild untuk mengambil nilai dari rightChild.
              return self.rightChild
          def getLeftChild(self): #GetLeftChild untuk mengambil nilai dari leftChild.
              return self.leftChild
          def setRootVal(self,obj): #untuk membuat key(parrent) baru.
              self.key = obj
          def getRootVal(self): #untuk mengambil nilai di dalam key(parrent).
              return self.key

      def buildParseTree(fpexp): #buildParseTree untuk membuat Tree dari deret aritmatika (seperti postfix)
          fplist = fpexp.split()
          pStack = Stack()
          eTree = BinaryTree('')
          pStack.push(eTree)
          currentTree = eTree
          for i in fplist:
              if i == '(':
                  currentTree.insertLeft('')
                  pStack.push(currentTree)
                  currentTree = currentTree.getLeftChild()
              elif i not in ['+', '-', '*', '/', ')']:
                  currentTree.setRootVal(int(i))
                  parent = pStack.pop()
                  currentTree = parent
              elif i in ['+', '-', '*', '/']:
                  currentTree.setRootVal(i)
                  currentTree.insertRight('')
                  pStack.push(currentTree)
                  currentTree = currentTree.getRightChild()
              elif i == ')':
                  currentTree = pStack.pop()
              else:
                  raise ValueError
          return eTree

      def postfix(tree): #postfix yaitu cara yang meletakkan operator di sebelah kanan 2 
          if tree != None:
              postfix(tree.getLeftChild())
              postfix(tree.getRightChild())
              print(tree.getRootVal(), end=' ')

      def postfixreval(tree):
          opers = {'+':operator.add, '-':operator.sub, '*':operator.mul, '/':operator.truediv}
          res1 = None
          res2 = None
          if tree:
              res1 = postfixreval(tree.getLeftChild())
              res2 = postfixreval(tree.getRightChild())
              if res1 and res2:
                  return opers[tree.getRootVal()](res1,res2)
              else:
                  return tree.getRootVal()

      pt = buildParseTree("( ( 8 + 9 ) * 2 )")
      postfix(pt)
      print()
      print(postfixreval(pt))
