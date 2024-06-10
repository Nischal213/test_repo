class Node:

    def __init__(self, data) -> None:
        self.data = data
        self.next = None


class LinkedList:

    # Singly Linked List

    def __init__(self) -> None:
        self.head = None
        self.size = 0

    def add_item(self, item):
        new_node = Node(item)
        if self.head is None:
            self.head = new_node
        else:
            current_node = self.head
            while current_node.next is not None:
                current_node = current_node.next
            current_node.next = new_node
        self.size += 1
        return "Successfully added item"

    def remove_item(self, item):
        if self.size == 0:
            return "Linked list is empty"
        else:
            current_node = self.head
            previous_node = None
            while current_node.data != item:
                previous_node = current_node
                current_node = current_node.next
                if current_node is None:
                    break

            if current_node is None:
                return "Item does not exist"
            if self.head.data == item:
                self.head = current_node.next
            else:
                previous_node.next = current_node.next
            self.size -= 1
            return "Item successfully removed"

    def insert_item(self, index, item):
        if index > self.size:
            return "Index out of linked list size"

        new_node = Node(item)
        self.index = index
        current_node = self.head
        previous_node = None
        while self.index != index:
            previous_node = current_node
            current_node = current_node.next
        previous_node.next = new_node
        new_node.next = current_node
        return "Item successfully added"

    def display(self):
        current = self.head
        while current is not None:
            print(f"{current.data} ---> ", end="")
            current = current.next
        print("None")
        print(f"Size of linked list: {self.size}")
        return


ins = LinkedList()
ins.add_item(0)
ins.add_item(1)
ins.add_item(2)
ins.insert_item(1, 3)
ins.display()
