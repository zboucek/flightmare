.. _add-new-objects:

Add New Objects
===============

Static Objects
--------------

Base \class for static objects. Inherit from this class for new objects.

.. code-block:: C++

  #pragma once

  #include "flightlib/common/types.hpp"

  namespace flightlib {
  class StaticObject {
  public:
    StaticObject(std::string id, std::string prefab_id)
      : id_(id), prefab_id_(prefab_id){};
    virtual ~StaticObject(){};

    // publich get functions
    virtual Vector<3> getPos(void) = 0;
    virtual Quaternion getQuat(void) = 0;
    virtual Vector<3> getSize(void) = 0;

    // public get functions
    const std::string getID(void) { return id_; };
    const std::string getPrefabID(void) { return prefab_id_; };


  protected:
    const std::string id_;
    const std::string prefab_id_;
  };

  }  // namespace flightlib

Gate
----

The gate inherits from the StaticObject \class. 
All objects that behave like gates can be loaded with it.
The ``id`` defines the name of the object within Flightmare and needs to be unique.
The ``prefab_id`` is the name of the prefab in the ``Resources`` folder within the Unity project.

.. code-block:: C++

  #pragma once

  #include "flightlib/objects/static_object.hpp"

  namespace flightlib {
  class StaticGate : public StaticObject {
  public:
    StaticGate(std::string id, std::string prefab_id);
    ~StaticGate(){};

    // publich set functions
    void setPosition(const Vector<3>& position) { position_ = position; };
    void setRotation(const Quaternion& quaternion) { quat_ = quaternion; };
    void setSize(const Vector<3>& size) { size_ = size; };

    // publich get functions
    Vector<3> getPos(void) { return position_; };
    Quaternion getQuat(void) { return quat_; };
    Vector<3> getSize(void) { return size_; };

  private:
    std::string id_;
    std::string prefab_id_;

    Vector<3> position_{0.0, 0.0, 0.0};
    Quaternion quat_{1.0, 0.0, 0.0, 0.0};
    Vector<3> size_{1.0, 1.0, 1.0};
  };

  }  // namespace flightlib

