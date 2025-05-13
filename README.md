# heap-pq
Implementing a min heap class and a priority queue class

// BinaryHeap class   for implemeenting the heap tree(min heap)
public class BinaryHeap {

        int[] heap;
        int size;

        BinaryHeap(int capacity) {
            heap = new int[capacity];
            size = 0;
        }

        boolean insertion(int value) {
            if (isFull()) {
                System.out.println("Heap full");
                return false;
            }
            heap[size] = value;
            System.out.println(value+ " has been added to heap1.");
            heapifyUp(size);
            size++;
            return true;
        }

        int deletion() {
            if (isEmpty()) {
                System.out.println("Heap empty");
                return -1;
            }
            int removed = heap[0];
            heap[0] = heap[size - 1];
            size--;
            if (size > 0) {
                heapifyDown(0);
            }
            System.out.println(removed + " has been removed from heap1.");
            return removed;
        }

        private void heapifyUp(int index) {
            while (index > 0 && heap[parent(index)] > heap[index]) {
                swap(parent(index), index);
                index = parent(index);
            }
        }

        private void heapifyDown(int index) {
            int smallest = index;
            int left = leftChild(index);
            int right = rightChild(index);

            if (left < size && heap[left] < heap[smallest]) {
                smallest = left;
            }
            if (right < size && heap[right] < heap[smallest]) {
                smallest = right;
            }

            if (smallest != index) {
                swap(index, smallest);
                heapifyDown(smallest);
            }
        }

        private int parent(int i) {
            return (i - 1) / 2;
        }

        private int leftChild(int i) {
            return 2 * i + 1;
        }

        private int rightChild(int i) {
            return 2 * i + 2;
        }

        private void swap(int i, int j) {
            int tmp = heap[i];
            heap[i] = heap[j];
            heap[j] = tmp;
        }

        boolean isEmpty() {
            return size == 0;
        }

        boolean isFull() {
            return size == heap.length;
        }

        int size() {
            return size;
        }

        void print() {
            if(isEmpty()){
                System.out.println("Queue is empty");
                return ;
            }
            for (int i = 0; i < size; i++) {
                System.out.print(heap[i] + " ");
            }
            System.out.println();
        }
        int[] getHeapArray() {
            return java.util.Arrays.copyOf(heap, size);
        }
    }

// class PQ for implementing priority queue 
    class PQ {
        BinaryHeap heap1;

        PQ(int capacity) {
            heap1 = new BinaryHeap(capacity);
        }

        boolean enqueue(int value) {
            return heap1.insertion(value);
        }

        int dequeue() {
            return heap1.deletion();
        }



        void print() {
            if (heap1.isEmpty()) {
                System.out.println("Priority Queue is empty.");
                return;
            }

            int[] copy = heap1.getHeapArray();
            java.util.Arrays.sort(copy);

            System.out.print("Priority Queue (sorted by priority): ");
            for (int value : copy) {
                System.out.print(value + " ");
            }
            System.out.println();
        }

        int size() {
            return heap1.size();
        }

        boolean isEmpty() {
            return heap1.isEmpty();
        }
    }



 
// main 
import java.util.Scanner;


// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        PQ pq = new PQ(100);  // Set capacity to 100

        int choice;
        do {
            System.out.println("\nPriority Queue Menu");
            System.out.println("1. Insert");
            System.out.println("2. Delete (min)");
            System.out.println("3. Print");
            System.out.println("4. Is Empty?");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter value to insert: ");
                    int value = scanner.nextInt();
                    pq.enqueue(value);
                    break;
                case 2:
                    int removed = pq.dequeue();
                    if (removed != -1) {
                        System.out.println("Removed: " + removed);
                    }
                    break;
                case 3:
                    pq.print();
                    break;
                case 4:
                    System.out.println( (pq.isEmpty()?"queue Is empty " :"queue Is not empty " ));
                    break;
                case 5:
                    System.out.println("Exiting program.");
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }

        } while (choice != 5);

        scanner.close();
    }
}



