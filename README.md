# angular.js
It is a internship assignament
<!DOCTYPE html>
<html lang="en" ng-app="myApp">
<head>
    <meta charset="UTF-8">
    <title>AngularJS CRUD Application</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <style>
        .container {
            margin-top: 50px;
        }
    </style>
</head>
<body>
<div class="container" ng-controller="MainController">
    <h2>Item List</h2>
    <table class="table">
        <thead>
        <tr>
            <th>Name</th>
            <th>Description</th>
            <th>Action</th>
        </tr>
        </thead>
        <tbody>
        <tr ng-repeat="item in items">
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>
                <button class="btn btn-primary btn-sm" ng-click="editItem(item)">Edit</button>
                <button class="btn btn-danger btn-sm" ng-click="deleteItem(item)">Delete</button>
            </td>
        </tr>
        </tbody>
    </table>

    <h2>Add/Edit Item</h2>
    <form ng-submit="saveItem()">
        <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" ng-model="itemForm.name" required>
        </div>
        <div class="form-group">
            <label>Description:</label>
            <textarea class="form-control" ng-model="itemForm.description" required></textarea>
        </div>
        <button type="submit" class="btn btn-primary">Save</button>
    </form>
</div>

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
<script>
    var app = angular.module('myApp', []);

    app.controller('MainController', function ($scope) {
        $scope.items = [
            {id: 1, name: 'Item 1', description: 'Description for item 1'},
            {id: 2, name: 'Item 2', description: 'Description for item 2'}
        ];
        $scope.itemForm = {};

        $scope.editItem = function (item) {
            $scope.itemForm = angular.copy(item);
        };

        $scope.saveItem = function () {
            if ($scope.itemForm.id) {
                // Edit existing item
                var index = $scope.items.findIndex(function (item) {
                    return item.id === $scope.itemForm.id;
                });
                $scope.items[index] = angular.copy($scope.itemForm);
            } else {
                // Add new item
                $scope.items.push({
                    id: $scope.items.length + 1,
                    name: $scope.itemForm.name,
                    description: $scope.itemForm.description
                });
            }
            $scope.itemForm = {};
        };

        $scope.deleteItem = function (item) {
            var index = $scope.items.indexOf(item);
            $scope.items.splice(index, 1);
        };
    });
</script>
</body>
</html>
