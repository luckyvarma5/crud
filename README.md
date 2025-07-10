# crud
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRUD</title>
    <link rel="icon" href="icon.png" type="image/x-icon">
    <style>
        body{
            background-color: orange;
            font-size: 1.5rem;
            text-align: center;
        }

        h2{
            color: purple;
            font-weight: bolder;
        }

        table{
            margin: 50px auto;
            width: ;
        }

        input::placeholder, input{
            color: purple;
            padding: 3px;
            background-color: lavender;
            border: none;
        }

        button{
            color: purple;
            background-color: lavender;
            border: none;
            padding: 3px;
        }

        input, button {
            border-radius: 5px;
}

        :is(button,input):hover{
            transform: scale(1.1);
            background-color: thistle;
        }

        input:focus, button:focus{
            outline: none;
            border: 2px solid purple;
        }

        th, td, tr{
            border: 1px solid purple;
            padding: 15px;
        }

        th{
            font-weight: bold;
            color: purple;
            font-family: cursive;
        }

        tr{
            color: purple;
            font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
        }
    </style>
</head>
<body>
    <h2>USER CRUD APP</h2>
    <form id="userForm">
        <input type="text" id="name" name="name" placeholder="Item Name" required>    
        <input type="number" id="book" name="book" placeholder="Price"required>
        <button type="submit">Enter</button>
    </form>

    <br>

    <table id="userTable">
        <thead>
            <tr>
                <th>Item Name</th>
                <th>Price</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <script>
        const userForm = document.getElementById('userForm');
        const nameInput = document.getElementById('name');
        const bookInput = document.getElementById('book');
        const userTableBody = document.querySelector('#userTable tbody');

        let users=[];       // creating and initializing an array to store the data
        let editIndex = null;


        userForm.addEventListener('submit', function(e){
            e.preventDefault();
            const name = nameInput.value.trim();
            const book = bookInput.value.trim();

            
            if(editIndex==null){
            users.push({name,book});
        } else{
            users[editIndex] = {name,book};
            editIndex = null;
        }

            userForm.reset();
            renderTable();
        });

        
        function renderTable() {
            userTableBody.innerHTML = '';
            users.forEach((user, index) => {
                const row = document.createElement('tr');

                row.innerHTML = `
                    <td>${user.name}</td>
                    <td>${user.book}</td>
                    <td>
                        <button onclick="editUser(${index})">Edit</button>
                        <button onclick="deleteUser(${index})">Delete</button>
                    </td> `;

                userTableBody.appendChild(row);
            });

            window.editUser = function(index) {
                const user = users[index];
                nameInput.value = user.name;
                bookInput.value = user.book;
                editIndex = index;
            }

            window.deleteUser = function(index) {
                if (confirm('Are you sure you want to delete this name?')){
                    users.splice(index, 1);
                    renderTable();
                }
            }
            
        }

    </script>
</body>
</html>
