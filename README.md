# NoSQL_ORM
A MongoDb Connection with CRUD operations

API Infos:

 @PostMapping("")
    public User createUser(@RequestBody User user){
        user.setId(null);
        return userRepository.save(user);
    }

    @GetMapping
    public List<User> getUsers(){
        return userRepository.findAll();
    }

    @GetMapping("/count")
    public long count(){
        return userRepository.count();
    }

    @GetMapping("/{id}")
    public User getUsers(@PathVariable String id) throws Exception{
        Optional<User> user = userRepository.findById(id);
        if(user.isPresent()){
            return user.get();
        }else{
            throw new Exception("User is not found");
        }
    }

    @PutMapping("/{id}")
    public User editUser(@PathVariable String id, @RequestBody  User user) throws Exception{
        if(!userRepository.existsById(id)) throw new Exception("User is not found");
        user.setId(id);
        return userRepository.save(user);
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable String id){
        userRepository.deleteById(id);
    }
