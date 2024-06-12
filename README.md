class Node:
    # A node is in the form
    # (data , pointer to next nodes)
    def __init__(self, data) -> None:
        self.data = data
        self.next = None


class LinkedList:
    # Implementing a singly linked list
    def __init__(self) -> None:
        self.head = None
        self.size = 0
    """
    Made with assistance from chatgpt
    """
    def add_item(self, item):
        new_node = Node(item)
        if self.head is None:
            # If the head pointer is empty then
            # the list is empty so we just make
            # the head point to the new node
            self.head = new_node
        else:
            # Iterating through all the nodes in
            # the list
            current_node = self.head
            while current_node.next is not None:
                current_node = current_node.next
            # The last node in the list should
            # point to the new node we added
            current_node.next = new_node
        self.size += 1
        return "Item successfully added"
    """
    Made by myself
    """
    def remove_item(self, item):
        if self.size == 0:
            return "Linked list is empty"
        # Iterating through all the nodes in
        # the list but also keeping track
        # of the node before the current node
        current_node = self.head
        previous_node = None
        while current_node.data != item:
            previous_node = current_node
            current_node = current_node.next
            # If the current node is None but the list
            # isn't empty , then this means the item doesn't
            # exist as we have already searched through all
            # the nodes
            if current_node is None:
                return "Item does not exist"
        # The item we want to remove is the first
        # element
        if current_node == self.head:
            # if this is the case then just make the head
            # point to the next element
            self.head = current_node.next
        else:
            # else, make the previous node point to the
            # current node's pointer
            previous_node.next = current_node.next
        self.size -= 1
        return "Item has been successfully removed"
    """
    Made by myself
    """
    def insert_item(self, index, item):
        # Indexing starts from zero this
        # indicates inserting item at the
        # beginning of the linked list
        if index > self.size:
            return "Index cannot be larger than list size"
        new_node = Node(item)

        if index == 0:
            # If inserting at the start of the list
            # Then , make the node point to the head
            # then , make the head point to the node
            new_node.next = self.head
            self.head = new_node
        else:
            # Increasing the counter until it reaches
            # the index wanted , taking into account of
            # current and previous nodes
            counter = 0
            current_node = self.head
            previous_node = None
            while counter != index:
                counter += 1
                previous_node = current_node
                current_node = current_node.next
            if counter == self.size:
                # If the counter has the same size as the list,
                # it means appending to the end
                # so , just make the last item's pointer point
                # to the new node
                previous_node.next = new_node
            else:
                # else , make the previous node's pointer point to
                # the current node and then make the new node's
                # pointer point to the current node
                previous_node.next = new_node
                new_node.next = current_node
        self.size += 1
        return "Item has been inserted successfully"
    """
    Made by chatgpt, although there is
    an alternate version made by me but
    it is less effficient
    """
    def reverse_list(self):
        if self.size >= 2:
            previous_node = None
            current_node = self.head
            while current_node is not None:
                next_node = current_node.next
                current_node.next = previous_node
                previous_node = current_node
                current_node = next_node
            self.head = previous_node
        return f"List has been succcessfully reversed"
    """
    Made by chatgpt
    """
    def sort_lst(self ,asc=True):
        if self.size < 2:
            return "List is too short to sort"
        if asc:
            # Basic bubble sort implementation
            change = True
            while change:
                change = False
                # Using the first item as the head
                current = self.head
                while current.next is not None:
                    # Storing the next node
                    next_node = current.next
                    if current.data > next_node.data:
                        # Swap the data
                        current.data, next_node.data = next_node.data, current.data
                        change = True
                    current = next_node
        else:
            change = True
            while change:
                change = False
                current = self.head
                while current.next is not None:
                    next_node = current.next
                    if current.data < next_node.data:
                        # Swap the data
                        current.data, next_node.data = next_node.data, current.data
                        change = True
                    current = next_node
        return "Successfully sorted the linked list"
    
    def length(self):
        return self.size
    
    def get_index(self,item):
        counter = 0
        current_node = self.head
        while current_node is not None:
            if current_node.data == item:
                return counter
            counter += 1
            current_node = current_node.next
        return -1
    
    def clear(self):
        self.head = None

    def display(self):
        current_node = self.head
        while current_node is not None:
            print(f"{current_node.data} --> ", end="")
            current_node = current_node.next
        print("None")
        print(f"The size of the linked list is {self.size}")
