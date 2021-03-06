<h1>Image Classification using CNNs</h1>
<h3>Team Members</h3>
  <ol>
    <li><strong>Rishanth. R</strong> (CS18B044)</li> 
  </ol>
  <h3>Important Note</h3>
  <p>
      Due to 100MB file size limit of Github, data files (train, validation and test set data, gradients data, inaturalist images folders) could not be uploaded in this github repository.
</p>
<p>
      Due to the large sizes of certain data files, the following error was encountered when trying to push code from local repository to online repository:<br/>
      <em>"fatal: the remote end hung up unexpectedly"</em><br/>
      Because of this error, several new folders had to be created and the original version control couldn't be retained in the current repository. 
</p>
<h3>Contents of the files</h3>
  <ul>
  <li>
    <strong>ConvNeuralNetwork.py</strong>
    <p>
      Contains the class definition for a Convolutional Neural Network with all the associated functions required to initialise a CNN, train the CNN over the training set while using the validation set to find the hyperparameters and to evaluate the model over the test set. 
    </p>
  </li>
  <li>
    <strong>generateData.py</strong>
    <p>
     Used to convert the given set of iNaturalist images into arrays which can be given as input to the CNN. 10% of the training set is used as validation set.
    </p>
    <p>
      The flag "-dataAug" should be set when the program is run to enable dataset augmentation.
    </p>
  </li>
  <li>
    <strong>train.py</strong>
    <p>
      Contains code to set up a CNN based on specified hyperparamters, train it over the training dataset and finally evaluate the model over the test set.<br/>
    </p>
    <p>
      By default, the program when run builds a CNN and trains it over the training dataset. To evaulate a previously build, trained and saved model (saved in ./best_model/best_model_acc), the flag "-eval" should be included while running the program.
    </p>
    <p>
      The onus is on the user to run the program with the "-eval" flag only after building, training the model and setting the hyperparameters_default (in the same file) with the values corresponding to the best model stored, to avoid errors.
    </p>
    <p>
       To do guided backpropagation of the outputs wrt the weights, the program should be run with the "-guidedBackProp" flag. It is assumed that the gradients have already been generated and stored at "./guidedBackPropGrads.npy". If the gradients have to be generated, a second flag "-generateGrads" has to be added while running the program.
      We visualise the gradients for 10 random images from the test dataset in sets of 2.
    </p>
    <p>
      To visualise the filters of the first layer over a random sample from the test set, run the program with the flag "-visualiseFilters".
    </p>
    <p>
      To predict classes for 10 random samples from the test set, run the program with the flag "-predictedClasses".
    </p>
  </li>
  <li>
    <strong>sweep.yaml</strong>
    <p>
      Contains the sweep configuration.<br/>
      The bayes strategy was chosen for the sweep over grid search (computationally expensive) and random search (might settle for local minima)<br/>
      Categorical accuracy of the validation set is used to tune the hyperparamters with the objective of maximising it.
    </p>
  </li>
  <li>
    The following files contain the array form of the input image data, generated by running 'generateData.py' using appropriate flags:
    <ul><b>
      <li>x_train.npy</li>
      <li>y_train.npy</li>
      <li>x_valid.npy</li>
      <li>y_valid.npy</li>
      <li>x_train_aug.npy</li>
      <li>y_train_aug.npy</li>
      <li>x_valid_aug.npy</li>
      <li>y_valid_aug.npy</li>
      <li>x_test.npy</li>
      <li>y_test.npy</li></b>
    </ul>
  </li>
  <li>
    The folder <b>'./best_model'</b> contains two subfolders:
    <ul>
      <li><b>best_model_acc</b> : best model based on validation categorical accuracy</li>
      <li><b>best_model_loss</b> : best model based on validation categorical loss</li>
    </ul>
  </li>
  <li>
    <b>visualise.py</b> : Used to visualise samples from the generated array representation of the input images
  </li>
 </ul>
<h3>Running the code</h3>
  <h5>Train and evaluate a convolutional neural network</h5>
  <p>
    To train a convolutional neural network based on a specific set of hyperparamters, one has to first modify the hyperparameters_default dictionary, defined in train.py, 
    appropriately.<br/>
    After logging into your wand accound using 'wandb login', run the command 'python3 train.py' in the project directory terminal in the terminal.<br/>
    The code initialises a convolutional neural network with the specified hyperparameters, and then trains the CNN over the training dataset.<br/>
    The code has to be run again with the flag "-eval" to evaluate the program over the test dataset.<br/>
    To perform guided backpropagation, train.py has to be run with the flag "-guidedBackProp". If the gradients haven't already been generated, also use the flag "-generateGrads"<br/>
    To visualise the filters of the first layer over a random sample from the test set, run the program with the flag "-visualiseFilters".<br/>
    To predict classes for 10 random samples from the test set, run the program with the flag "-predictedClasses".
  </p>
  <h5>Run a sweep</h5>
  <p>
    Run the command 'wandb sweep sweep.yaml' in the project directory in the terminal.<br/>
    Then run the command 'wandb agent %sweep-agent-generated-by-previous-command-here%' to start the sweep.
  </p>

