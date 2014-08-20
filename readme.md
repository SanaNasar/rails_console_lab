## Console Lab

For this lab, we'd like you to strengthen your Rails console skills. This lab is going to be very familiar to the SQL lab, where we'll ask you to create a model and then write out the console commands you would use to execute these queries

### To Start

1. Create a model called Student, that has a first_name, last_name and age
	
		Student.new(:first_name => "Jane", :last_name => "Doe", :age => 22)


2. Don't forget to run your migrations
	
		student.save

### Tasks to create

1. Using the new/save syntax, create a student, first and last name and an age
	
		Student.new(:first_name => "Jane", :last_name => "Doe", :age => 22)
		
2. Save the student to the database
	
		student.save
	
3. Using the find/set/save syntax update the student's first name to taco
	
		student = Student.find(1)
	
		student.first_name = "Taco"
	
		student.save

4. Delete the student (where first_name is taco)
	
		student = Student.find(1)

		student.destroy

5. Validate that every Student's last name is unique
	
		validates :last_name, :uniqueness => true

6. Validate that every Student has a first and last name that is longer than 4 character
	
		:first_name, :length => {:minimum => 4}

7. Validate that every first and last name cannot be empty
	
		validates_presence_of :first_name, :last_name

8. Combine all of these individual validations into one validation (using validate and a hash) 

		validates :first_name, :last_name, :presence => true, :length => {:minimum => 4}, :uniqueness => true
	
9. Using the create syntax create a student named John Doe who is 33 years old
	
		Student.create({:first_name => 'John', :last_name => "Doe", age: 33})
	
10. Show if this new student entry is valid
	
		student.valid?
	
11. Show the number of errors for this student instance
	
		student.errors.count (or) john.errors.size
	
12. In one command, Change John Doe's name to Jonathan Doesmith

		student = Student.find_by_last_name("Doe") student.update_attribute(:last_name => "Doesmith")
	
13. Clear the errors array

		student.error.clear
	

13. Save Jonathan Doesmith
	
		student.save
	
14. Find all of the Students
	
		Student.all
	
15. Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error
		
		Student.find_by_id(128)

	
16. Find the first student in the table
	
		Student.first
	
17. Find the last student in the table
	
		Student.last
		
18. Find the student with the last name of Doesmith

		Student.find_by_last_name("Doesmith")
	
19. Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order
	
		Student.all.limit(5).offset(1).order(last_name: :asc)


20. Delete Jonathan Doesmith

		student = Student.find_by_last_name('Doesmith')
		//find the person
		student.destroy()
		//then destroy it

### Bonus
1. Use the validates_format_of and regex to only validate names that consist of letters (no numbers or symbols) and start with a capital letter

		validates_format_of :first_name, :last_name, :with => /\A[A-Z][a-z]{3,}\z/ 
[Rubular](http://rubular.com)
	
2. Write a custom validation to ensure that no one named Delmer Reed, Tim Licata, Anil Bridgpal or Elie Schoppik is included in the students table

		FORBIDDEN_NAMES = [
	    		["Anil", "Bridgpal"],
	    		["Elie", "Schoppik"],
	    		["Delmer", "Reed"],
	    		["Tim", "Licata"]
  		]
  		validate :name_is_allowed

  		def name_is_allowed
    			FORBIDDEN_NAMES.each do |name|
	      			if name[0].include?(first_name) &&
	      			name[1].include?(last_name)
	          		errors.add(:name,"you are a restricted
	          		user")
      				end
    			end
  		end


