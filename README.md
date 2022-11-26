# Pokemon-Game
/* program for a Pokémon Game. Your program should allow 2 players to choose 3 Pokémons and then compete with each other. Your program will take a text file (Pokemons.txt) as an input which contains all Pokémons information.
The basic functionality of the Pokémon list will be implemented using a linked list. Each node in the list contains one Pokémon object, and a pointer to the next node.
       Hints:
•	To read the input file use Scanner class
•	To iterate over each string in the file use Scanner.next() method
•	You need to read from the file (Pokemons.txt) to fill the linked list.
    Implementation
     For this program you will create 8 classes as follows:
•	Pokemon.java: This class will be used to create objects of type Pokémon. Each Pokémon object will store one Pokémon information.
•	PokemonLLNode.java: This class will be used to create a linked list node. Each node contains one Pokémon object, and a pointer to the next node.
•	PokemonLL.java: This class will be used to create a linked list with nodes of type PokemonLLNode. Most of the methods will be implemented in this class.
•	PokemonQueue.java: This class will be used to create a Queue for Pokémons. This queue will be used to store the Pokémons of each player.
•	PokemonStack.java: This class will be used to create a Stack for Pokémons. This stack will be used to reverse the Pokémons of each player.
•	PokemonBSTNode.java: This class will be used to create a binary search tree node. Each node contains one Pokémon object, a pointer to the left child node, and a pointer to the right child node.
•	PokemonBST.java: This class will be used to create a binary search tree with nodes of type PokemonBSTNode. This tree will be used to sort the Pokémons list.
•	PokemonGame.java: This is the class that will contain your main method.
 */
 
     public class Pokemon {
    private int id;
    private String name;
    private String type;
    private int attack;
    private int defense;
    private int total;

    public Pokemon(int id, String name, String type, int attack, int defense, int total) {
        this.id = id;
        this.name = name;
        this.type = type;
        this.attack = attack;
        this.defense = defense;
        this.total = total;
    }

    public Pokemon() {
    }

    public int getId() {
        return id;
    }


    public String getName() {
        return name;
    }


    public String getType() {
        return type;
    }


    public int getAttack() {
        return attack;
    }

    public int getDefense() {
        return defense;
    }


    public int getTotal() {
        return total;
    }

    @Override
    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Type: " + type + ", Attack: " + attack + ", Defense: " + defense + ", Total: " + total;

    }
      }
    public class PokemonBST {
    private PokemonBSTNode root;

    public void insert(Pokemon data) {
        if(isEmpty())
            root = new PokemonBSTNode(data);
        else
            insert(root, new PokemonBSTNode(data));
    }
    private void insert(PokemonBSTNode node, PokemonBSTNode newNode) {
        if(node.getPokemon().getTotal() > newNode.getPokemon().getTotal()) {
            if(node.getLeft() == null)
                node.setLeft(newNode);
             else
                insert(node.getLeft(), newNode);
        } else if(node.getRight() == null)
                node.setRight(newNode);
             else
                insert(node.getRight(), newNode);
    }
    // check leaf node
    public boolean isLeaf(PokemonBSTNode node) {
        return node.getLeft() == null && node.getRight() == null;
    }
    // check if node has one child
    public boolean hasOneChild(PokemonBSTNode node) {
        return node.getLeft() == null || node.getRight() == null;
    }
    // check if node has two children
    public boolean hasTwoChildren(PokemonBSTNode node) {
        return node.getLeft() != null && node.getRight() != null;
    }
    // delete node with id 
    public void delete(int id) {
        if(isEmpty())
            throw new IllegalStateException("Tree is empty");
        else
            delete(root, id);
    }
    private PokemonBSTNode delete(PokemonBSTNode node, int id) {
        if(node == null)
            return null;
        if(node.getPokemon().getId() == id) {
            if(isLeaf(node))
                return null;
            else if(hasOneChild(node))
                return node.getLeft() == null ? node.getRight() : node.getLeft();
            else {
                PokemonBSTNode temp = node.getRight();
                while(temp.getLeft() != null)
                    temp = temp.getLeft();
                node.setPokemon(temp.getPokemon());
                node.setRight(delete(node.getRight(), temp.getPokemon().getId()));
            }
        } else if(node.getPokemon().getId() > id)
            node.setLeft(delete(node.getLeft(), id));
        else
            node.setRight(delete(node.getRight(), id));
        return node;
    }
    public boolean isEmpty() {
        return root == null;
    }
    public void inOrder(){
        inOrder(root);
    }
    private void inOrder(PokemonBSTNode node) {
        if(node == null) return;

        inOrder(node.getLeft());
        System.out.println(node.getPokemon());
        inOrder(node.getRight());
    }
    
    public void preOrder(){
        preOrder(root);
    }
    private void preOrder(PokemonBSTNode node) {
        if(node == null) return;

        System.out.println(node.getPokemon());
        preOrder(node.getLeft());
        preOrder(node.getRight());
    }
    
    public void postOrder(){
        postOrder(root);
    }
    private void postOrder(PokemonBSTNode node) {
        if(node == null) return;

        postOrder(node.getLeft());
        postOrder(node.getRight());
        System.out.println(node.getPokemon());
    }
       }
       public class PokemonBSTNode {
    private PokemonBSTNode left;
    private PokemonBSTNode right;

    private Pokemon pokemon;

    public PokemonBSTNode(Pokemon data) {
        this.pokemon = data;
    }

    public PokemonBSTNode getLeft() {
        return left;
    }

    public void setLeft(PokemonBSTNode left) {
        this.left = left;
    }

    public PokemonBSTNode getRight() {
        return right;
    }

    public void setRight(PokemonBSTNode right) {
        this.right = right;
    }

    public Pokemon getPokemon() {
        return pokemon;
    }
    public void setPokemon(Pokemon pokemon) {
        this.pokemon = pokemon;
    }

    }
       public class PokemonLL {
    private PokemonLLNode head;

    public boolean isEmpty() {
        return head == null;
    }

    // append to the end of the list
    public void add(Pokemon pokemon) {
        PokemonLLNode node = new PokemonLLNode(pokemon);
        if (isEmpty())
            head = node;
        else {
            PokemonLLNode current = head;
            while (current.getNext() != null)
                current = current.getNext();
            current.setNext(node);
        }
    }
    public void addFirst(Pokemon pokemon){
        PokemonLLNode node = new PokemonLLNode(pokemon);
        if (!isEmpty())
            node.setNext(head);
        head = node;
    }

    public int size(){
        int count = 0;
        PokemonLLNode current = head;
        while (current != null) {
            count++;
            current = current.getNext();
        }
        return count;
    }
    public Pokemon get(int index){
        if (index < 0 || index >= size())
            return null;
        PokemonLLNode current = head;
        for (int i = 0; i < index; i++)
            current = current.getNext();
        return current.getPokemon();
    }
    public Pokemon getPokemonWithId(int id){
        PokemonLLNode current = head;
        while (current != null) {
            if (current.getPokemon().getId() == id)
                return current.getPokemon();
            current = current.getNext();
        }
        return null;

    }
    public String basicInfo(){
        String info = "Total number of pokemons = "+size();
        if(isEmpty())return info;

        int numberOfElectric = 0,numberOfFire = 0,numberOfWater = 0,numberOfGrass = 0,max = Integer.MIN_VALUE;

        Pokemon strongest = null;
        double sum = 0;

        PokemonLLNode current = head;
        while (current != null) {
            if (current.getPokemon().getType().equals("Electric"))
                numberOfElectric++;
            else if (current.getPokemon().getType().equals("Fire"))
                numberOfFire++;
            else if (current.getPokemon().getType().equals("Water"))
                numberOfWater++;
            else if (current.getPokemon().getType().equals("Grass"))
                numberOfGrass++;

            if(current.getPokemon().getTotal() > max){
                max = current.getPokemon().getTotal();
                strongest = current.getPokemon();
            }
            sum += current.getPokemon().getTotal();
            current = current.getNext();
        }

        info +="\nNumber of Electric pokemons = "+numberOfElectric;
        info +="\nNumber of Grass pokemons = "+numberOfGrass;
        info +="\nNumber of Fire pokemons = "+numberOfFire;
        info +="\nNumber of Water pokemons = "+numberOfWater;
        info +="\nThe strongest pokemon is "+strongest.getName();
        info +="\nThe average of all pokemons power is "+(sum/size());
        return info;
    }

     }
     public class PokemonLLNode {
    private Pokemon pokemon;
    private PokemonLLNode next;

    public PokemonLLNode(Pokemon pokemon) {
        this.pokemon = pokemon;
    }

    public Pokemon getPokemon() {
        return pokemon;
    }

    public PokemonLLNode getNext() {
        return next;
    }

    public void setNext(PokemonLLNode next) {
        this.next = next;
    }
    }
    public class PokemonQueue {
    private Pokemon[] queue;
    private int maxSize;
    private int front;
    private int numItems;

    public PokemonQueue(int size) {
        maxSize = size;
        queue = new Pokemon[maxSize];
    }
    public void enqueue(Pokemon data) {
        if (isFull())
            throw new IllegalStateException("Queue is full");
        queue[numItems++] = data;
    }
    public boolean isFull(){
        return numItems == maxSize;
    }
    public boolean isEmpty(){
        return numItems == 0;
    }
    public Pokemon dequeue() {
        if (isEmpty())
            throw new IllegalStateException("Queue is empty");
        // circular queue
        Pokemon temp = queue[front];
        queue[front] = null;
        front = (front + 1) % maxSize;
        numItems--;
        return temp;
    }
    public Pokemon peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return null;
        }
        return queue[front];
    }
    public void display() {
        for (int i = 0; i < numItems; i++)
            System.out.print(queue[i].getName()+", ");
        System.out.println();
    }
    public void clear() {
        queue = new Pokemon[maxSize];
        front = 0;
        numItems = 0;
    }
    }
    public class PokemonStack {
    private Pokemon[] stack;
    private int maxSize;
    private int top;

    public PokemonStack(int size) {
        maxSize = size;
        stack = new Pokemon[maxSize];
    }
    public void push(Pokemon data) {
        if (isFull())
           throw new StackOverflowError("Stack is full");
        stack[top++] = data;
    }
    public boolean isFull(){
        return top == maxSize;
    }
    public boolean isEmpty(){
        return top == 0;
    }
    public Pokemon pop() {
        if (isEmpty())
            throw new IllegalStateException("Stack is empty");
        return stack[--top];
    }
    public Pokemon top() {
        if (isEmpty())
            throw new IllegalStateException("Stack is empty");
        return stack[top - 1];
    }
    }
//Main



                      import java.io.File;
                      import java.io.FileNotFoundException;
             import java.util.Scanner;



     public class PokemonGame {
    private static Scanner read;
    private static PokemonLL pokemonList;
    private static PokemonBST pokemonBST;
    private static PokemonQueue player1;
    private static PokemonQueue player2;
    public static void main(String[] args) throws FileNotFoundException {
        File file = new File("Pokemons.txt");
        if(!file.exists()){
            System.out.println("Sorry input file does not exist");
            return;
        }
        pokemonList = new PokemonLL();
        pokemonBST = new PokemonBST();
        read = new Scanner(file);

        System.out.println(
                "**************************************************************************\n" +
                "****                     Welcome to Pokemon Game                      ****\n" +
                "**************************************************************************\n" +
                "Pokemons Information...");

        // read pokemon data from file
        while (read.hasNext()) {
            Pokemon pokemon = new Pokemon(read.nextInt(), read.next(), read.next(), read.nextInt(), read.nextInt(),read.nextInt());
            pokemonList.add(pokemon);
            pokemonBST.insert(pokemon);
            System.out.println(pokemon);
        }
        System.out.println("\n"+pokemonList.basicInfo());
        System.out.println("\nPokemons from weakest to strongest..");
        pokemonBST.inOrder();
        System.out.println("*********************************");

        System.out.println("\nWe want to make a competition between 2 players\n" +
                "Each player should choose 3 pokemons to fight with");
        System.out.println("Enter the name of the first player:");
        // reassign the variable 'read' to read from the keyboard as we want to read the name of the players
        read = new Scanner(System.in);
        String firstPlayer = read.nextLine();
        System.out.println("Enter the name of the second player:");
        String secondPlayer = read.nextLine();


        System.out.println("\nNow, each player should choose 3 pokemons");
        System.out.println("your first choice will play the first round and so on..");
        System.out.println("Start with "+firstPlayer);
        player1 = choosePokemon();
        System.out.println("\nNow, "+secondPlayer+" turn");
        player2 = choosePokemon();
        System.out.println();
        System.out.println(firstPlayer+" Army.. ");
        player1.display();
        System.out.println(secondPlayer+" Army.. ");
        player2.display();

        System.out.println("\nLet The Battle Starts...");
        int result = fight(1);
        System.out.println("The Final Result of Battale...");
        if(result > 0)
            System.out.println(firstPlayer+" Wins..");
        else if(result < 0)
            System.out.println(secondPlayer+" Wins..");
        else
            System.out.println("It's a Tie..");

        System.out.println("\nHope you enjoy our Pokemon game:)");
        System.out.print("See you in next games..");
    }

    private static PokemonQueue choosePokemon() {
        PokemonQueue player = new PokemonQueue(3);
        for (int i = 1; i <= 3; i++) {
            System.out.println("Enter the id of pokemon "+i);
            Pokemon pokemon = pokemonList.getPokemonWithId( read.nextInt());
            if(pokemon == null){
                System.out.println("Wrong pokemon id!!");
                i--;
                continue;
            }
            player.enqueue(pokemon);
        }
        System.out.println("Do you want to reverse your pokemons (y/n)?");
        if(read.next().equalsIgnoreCase("y")) {
            PokemonStack stack = new PokemonStack(3);
            while (!player.isEmpty())
                stack.push(player.dequeue());
            while (!stack.isEmpty())
                player.enqueue(stack.pop());
        }
        return player;
    }
    public static int fight(int round){
        if(round > 3)return 0;
        Pokemon pokemon1 = player1.dequeue();
        Pokemon pokemon2 = player2.dequeue();
        System.out.println("Round "+round);
        if(pokemon1.getAttack() > pokemon2.getDefense() && pokemon1.getDefense() > pokemon2.getAttack()) {
            System.out.println(pokemon1.getName() + " Wins!!");
            return 1 + fight(round + 1);
        }
        else if(pokemon2.getAttack() > pokemon1.getDefense() && pokemon2.getDefense() > pokemon1.getAttack()) {
            System.out.println(pokemon2.getName() + " Wins!!");
            return -1 + fight(round + 1);
        }
        else {
            System.out.println("it is a Tie..");
            return fight(round + 1);
        }
    }
}

